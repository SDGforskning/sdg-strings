# Search query for SDG13 - Climate Action, Bergen action-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG13
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes


## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG13</summary>

```
TS=( ( ("educati*" OR "curriculum" OR "curricula" OR "institutional capacity" OR "human capacity" OR "systemic capacity" OR "awareness" OR "perception$" OR "technical knowledge transfer" OR "transfer of technical knowledge" OR "transfer of technolog*" OR "technology transfer$" OR "official development assistance" OR "official development aid" OR "foreign aid" OR "international aid" OR "cooperation fund" OR "investment$" OR "invest" OR "investing") NEAR/15 ( (("climate change$" OR "global warming" OR "climatic change$") NEAR/15 ("mitigat*" OR "adapt*" OR "impact reduction" OR "early warning" OR "risk$") ) OR "climate mitigation" ) ) OR "Green climate fund" OR "climate action$" OR "climate governance" OR "climate mitigation" OR (("climate change$" OR "global warming" OR "climatic change$" OR "changing climate" OR (("climate" OR "atmospher*" OR "ocean") NEAR/3 "warming") OR (("sea ice*" OR "sea-ice" OR "glaci*") NEAR/5 ("melt*" OR "retreat*"OR "reced*")) OR ("permafrost" NEAR/3 ("degrada*" OR "decreas*" OR "melt*")) ) NEAR/10 ("action$" OR "sustainab*" OR "assessment$" OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*" OR "impact reduction" OR (("reduc*" OR "minimi*" OR "decreas*" OR "limit" OR "alleviat*" OR "mitigat*") NEAR/2 ("impact$" OR "effect$")) OR "planning" OR "strateg*" OR "manag*" OR "policy" OR "policies" OR "legislat*" OR "govern*" OR "disaster risk reduction" OR "preparedness" ) ) OR ( ("reduc*" OR "combat*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "alleviat*" OR "tackl*" OR "lower" OR "mitigat*" OR "prevent*" OR "stop*" OR "avoid*" ) NEAR/5 ("GHG" OR "greenhouse gas" OR "greenhouse gases" OR "carbon footprint" OR ("climate" NEAR/5 ("anthropogenic" OR "human impact$")) ) ) OR (( ("reduc*" OR "combat*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "alleviat*" OR "tackl*" OR "lower" OR "mitigat*" OR "prevent*" OR "stop*" OR "avoid*" ) NEAR/5 ("methane" OR "CH4" OR "nitrous oxide" OR "N2O" OR "carbon dioxide" OR "CO2" OR "carbon emissions" OR "hydrofluorocarbons" OR "HFCs" OR "perfluorocarbons" OR "PFCs" OR "sulphur hexafluoride" OR "sulfur hexafluoride" OR "SF6") ) AND ("climate change$" OR "climatic change$" OR "global warming" OR "changing climate" OR (("climate" OR "atmospher*" OR "ocean") NEAR/3 "warming") ) ) OR ((( ("combat*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "prevent*" OR "stop*" OR "avoid*" OR "adapt*" OR "resilien*" OR "cope" OR "coping" OR "vulnerab*" OR "preparedness" OR "mitigat*" OR "early warning" OR "policy" OR "policies" OR "protect*" OR (("disaster$" OR "risk$") NEAR/3 ("plan*" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "medical response$")) ) NEAR/15 ("hazard*" OR "catastroph*" OR "disaster*" OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation")) OR "drought$" OR "flood*" OR "collaps*" OR "tipping point" OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) ) ) OR "Livelihood Vulnerability Index" ) AND ("climate change$" OR "climatic change$" OR "global warming" OR "changing climate" OR (("climate" OR "atmospher*" OR "ocean") NEAR/3 "warming")) ) OR ("Kyoto protocol" OR "Paris Agreement" OR "COP 21" OR "COP21" OR "COP 22" OR "COP22" OR "COP 23" OR "COP23" OR "COP 24" OR "COP24" OR "UNFCCC" OR "United Nations Framework Convention on Climate Change" ) OR ("SDG13" OR "SDG$ 13" OR "SDG-13" OR "sustainable development goal$ 13" OR (("sustainable development goal$" OR "SDG$" OR "goal 13") NEAR/15 "climate")) )
```
</details>

## 2. General notes

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

* Definition of "capacity" : "[...] the ability of people, organizations and society as a whole to manage their affairs successfully"<sup id="UNDGcapacity">[2](#f2)</sup>.
* Definition of "capacity development" : "the process whereby people, organizations and society as a whole unleash, strengthen, create, adapt, and maintain capacity over time, in order to achieve development results"<sup id="UNDGcapacity">[2](#f2)</sup>.
* Most of the terminalogy/definition is taken from https://www.undrr.org/terminology/hazard

## 3.Targets

## Target 13.1

> **13.1 Strengthen resilience and adaptive capacity to climate-related hazards and natural disasters in all countries**
>
>13.1.1 Number of deaths, missing persons and directly affected persons attributed to disasters per 100,000 population
>
>13.1.2 Number of countries that adopt and implement national disaster risk reduction strategies in line with the Sendai Framework for Disaster Risk Reduction 2015–2030
>
>13.1.3 Proportion of local governments that adopt and implement local disaster risk reduction strategies in line with national disaster risk reduction strategies

This query consists of 1 phrase.

``` Ceylon =
TS=
(
  (
    (
      (
      "combat*" OR "prevent*" OR "stop*" OR "avoid* "OR "adapt*" OR "resilien*" OR "cope" OR "coping" OR "preparedness" 
      OR "mitigat*" OR "early warnin$" OR "policy" OR "policies" OR "protect*"  
      OR(("disaster$" OR "risk$") NEAR/3 ("plan*" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "medical response$"))
      OR
        (
        ("minimi*" OR "limit" OR "limiting" OR "decreas*") 
         NEAR/5 ("impact$" OR "risk$" OR "cosequence$" OR "effect*" OR "influence$" OR "vulnerab*")
        )
         
      )
      NEAR/15
          (
          (
          ("natural" OR "anthropogenic" OR "environmental" OR "climat$" OR "man-made") 
          NEAR/3 ("hazard*" OR "catastroph*" OR "disaster*")
          )
          OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$"))
          OR "drought$" OR "flood*" OR "heatwave$" OR "heat-wave$"OR "cold spells"
          OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" 
          OR "storm$"
          OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$"
          OR "landslide$" OR "rockslide$" OR "surface collapse$" OR "mud flow$"
          OR "land-slide$" OR "rock-slide$" OR "mud-flow$"
          OR "tipping point$"  
          OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
          )
    )
  OR "livelihood vulnerability index"
  )
 
)
```


## Target 13.2 

This query consists of 5 phrase.

> **13.2 Integrate climate change measures into national policies, strategies and planning**
>
>13.2.1 Number of countries with nationally determined contributions, long-term strategies, national adaptation plans and adaptation communications, as reported to the secretariat of the United Nations Framework Convention on Climate Change
>
>13.2.2 Total greenhouse gas emissions per year		

##### Phrase 1: 
"Climate mitigation" and similar as searchterm alone

``` Ceylon =
TS=
(
  "climate action$" OR "climate governance" OR "climate mitigation" OR "climate change adaptation$" OR "climate adaptation plan$"
   OR (("climate change$" OR "global warming" OR "climatic change$" OR "changing climate") NEAR/5  ("action$" OR "sustainab*" OR "assessment$"
      OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*"))
)

```
##### Phrase 2: 

Climate change devided in indicators of climate change:
global mean surface temperature, global ocean heat content, state of ocean acidification, glacier mass balance, Arctic and Antarctic sea-ice extent, global CO2 fraction and global mean sea level (https://library.wmo.int/doc_num.php?explnum_id=10618)

``` Ceylon =

TS=
(
  (("climate" OR "atmospher*" OR "ocean") NEAR/3 "warming")
  OR (("global temperature" OR "surface temperature") NEAR/3 ("increas*" OR "rise"))
  OR (("sea ice*" OR "sea-ice" OR "glaci*") NEAR/5 ("melt*" OR "retreat*" OR "reduc*" OR "decreas'"))
  OR ("permafrost" NEAR/3 ("degrada*" OR "decreas*" OR "melt*"))
  OR (("sea-level" OR "sea level") NEAR/3 ("increas*" OR "rise"))
  OR (("ocean acidification" OR "ocean heat content") NEAR/3 ("reduc*" OR "minimi*" OR "decreas*" OR "limit" OR "alleviat*"))
    )
  NEAR/10
        (
          ("reduc*" OR "minimi*" OR "decreas*" OR "limit" OR "alleviat*")
          NEAR/2 ("impact$" OR "effect$" OR "cosequence$" OR "effect*" OR "influence$" OR "vulnerab*")          
        )
      OR ("national" NEAR/5 ("program*"OR "strateg*"OR "policy" OR "policies")) 
      OR "govern*" OR "disaster risk reduction" OR "preparedness"
       )
)
```
##### Phrase 3:

Reduction of GHGs = main climate mitigation according to UNEP definition

``` Ceylon =
TS=
(
  ("reduc*" OR "combat*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "alleviat*" OR "tackl*" OR "lower" OR "mitigat*" OR "prevent*" OR "stop*" OR "avoid*"
  )
  NEAR/5
      ("GHG" OR "greenhouse gas" OR "greenhouse gases"
      OR "carbon footprint"
      OR ("climate" NEAR/5 ("anthropogenic" OR "human impact$"))
      )
)
```

##### Phrase 4:
The second part of this phrase covers the six main greenhouse gases (covered by the Kyoto Protocol) as listed in the 2014 IPCC Synthesis Report<sup id="IPCC2014">[3](#f4)</sup>.
this parts need to be linked to climate change 
 

``` Ceylon =
TS=
(
  (
    ("reduc*" OR "combat*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "alleviat*" OR "tackl*" OR "lower" OR "mitigat*" OR "prevent*" OR "stop*" OR "avoid*"
    )
    NEAR/5
        ("methane" OR "CH4" OR "nitrous oxide" OR "N2O" OR "carbon dioxide" OR "CO2" OR "carbon emissions"
        OR "hydrofluorocarbons" OR "HFCs" OR "perfluorocarbons" OR "PFCs" OR "sulphur hexafluoride" OR "sulfur hexafluoride" OR "SF6"
        )
  )
  AND
    ("climate change$" OR "climatic change$" OR "global warming" OR "changing climate"
    OR (("climate" OR "atmospher*" OR "ocean") NEAR/3 "warming")
    )
)
```

##### Phrase 5:

Frameworks for action are included, as documents referencing these are likely to be discussing climate action (i.e. applied climate science rather than basic). This does pick up some results to do with energy transitions, but generally as related to climate. IPCC not included as their scenarios are referred to as a reference very often and in fields not necessarily directly contributing to the targets.

``` Ceylon =
TS=
(
  "Kyoto protocol"
  OR "Paris Agreement"
  OR "COP 21" OR "COP21" OR "COP 22" OR "COP22" OR "COP 23" OR "COP23" OR "COP 24" OR "COP24"
  OR "UNFCCC" OR "United Nations Framework Convention on Climate Change"
)
```

Carbon capture/storage technology can contribute to climate mitigation (i.e. reduction of GHG) but in order to be consistent with our target interpretation method, any papers concerning it must relate the work to climate mitigation or reductions of GHG to be included. The same would apply to reforestation or other mitigation measures. Thus these are not included as individual search terms but are included in the given phrases.

## Target 13.b

> **13.b Promote mechanisms for raising capacity for effective climate change-related planning and management in least developed countries and small island developing States, including focusing on women, youth and local and marginalized communities**
>
>13.b.1 Number of least developed countries and small island developing States with nationally determined contributions, long-term strategies, national adaptation plans and adaptation communications, as reported to the secretariat of the United Nations Framework Convention on Climate Change


Covered by phrase 1 &  2 from target 13.2


## Target 13.3 & 13.a								

> **13.3 Improve education, awareness-raising and human and institutional capacity on climate change mitigation, adaptation, impact reduction and early warning**
>
>13.3.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

> **13.a Implement the commitment undertaken by developed-country parties to the United Nations Framework Convention on Climate Change to a goal of mobilizing jointly $100 billion annually by 2020 from all sources to address the needs of developing countries in the context of meaningful mitigation actions and transparency on implementation and fully operationalize the Green Climate Fund through its capitalization as soon as possible**
>
>13.a.1 Amounts provided and mobilized in United States dollars per year in relation to the continued existing collective mobilization goal of the $100 billion commitment through to 2025

Re target 13.3 - Interpretatation of what should be considered as contributing to "human and institutional capacity" is challenging - according to the UNDG definition, it concerns anything that would increase the ability of people and institutions to successfully manage climate change mitigation, adaption, impact reduction and early warning. Here consider we that all research on these topics would contribute, and therefore they do not have to be combined with the concept of capacity.

This query consists of 1 phrase.

##### Phrase 1:

`Green climate fund` is a dedicated climate fund.

``` Ceylon =
TS=
(
  (
    ("educati*" OR "curriculum" OR "curricula"
    OR "institutional capacity" OR "human capacity" OR "systemic capacity"
    OR "awareness" OR "perception$"
    OR "technical knowledge transfer" OR "transfer of technical knowledge" OR "transfer of technolog*" OR "technology transfer$"
    OR "official development assistance" OR "official development aid" OR "foreign aid" OR "international aid" OR "cooperation fund" OR "investment$" OR "invest" OR "investing"
    )
    AND
        ("climate mitigation"
        OR
          (
            ("climate change$" OR "global warming" OR "climatic change$")
            NEAR/15
                ("mitigat*" OR "adapt*" OR "impact reduction" OR "early warning" OR "risk$")
          )
        )
  )
  OR "green climate fund"
)

```


## General SDG

``` Ceylon =
TS=
(
  "SDG13" OR "SDG$ 13" OR "SDG-13" OR "sustainable development goal$ 13"
  OR
    (
      ("sustainable development goal$" OR "SDG$" OR "goal 13")
      NEAR/15 "climate"
    )
)
```

## 4. Authorship and review

## 5. Footnotes

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

Old format - I suggest we change to author-date

<b id="f2">2</b> United Nations Development Group (2017) Capacity Development, UNDAF companion guidance. https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance [accessed 19.12.2019] [↩](#UNDGcapacity)

<b id="f3">3</b> IPCC, 2014: Climate Change 2014: Synthesis Report. Contribution of Working Groups I, II and III to the Fifth Assessment Report of the Intergovernmental Panel on Climate Change [Core Writing Team, R.K. Pachauri and L.A. Meyer (eds.)]. IPCC, Geneva, Switzerland, 151 pp. [↩](#IPCC2014)
