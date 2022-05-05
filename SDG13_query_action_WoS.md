# Search query for SDG13 - Climate Action, Bergen action-approach.

Take urgent action to combat climate change and its impacts.

***Current status**: This string is currently under active development to improve the phrases and structure. It is substantially changed from the original version it was based on (v2019.11). "Full query" not updated.*

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG13
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes


## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG13 (not updated!)</summary>

```

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

This target is interpreted to cover research about how to strengthen resilience to climate-related hazards and natural disasters. Strategies dealing with climate-related hazards and natural disasters and how to minimize impact of climate-related hazards and natural disasters are considered to be a method to improve resilience. 

For climate-related hazards and natural disasters both generel terms (phrase 1) and specific hazards/desasters (phrase 2) are used.
This query consists of 2 phrases.

##### Phrase 1: 

Action: strengthen/improve OR establish "risk planning" 

Basic structure: (strengthen/improve reslience OR "risk planning" ) + disasters

Disasters contain both general terms and specific desasters


``` Ceylon =
TS=
(
  (
    (
      ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR 
      "develop" OR "developing" OR "implement"
       OR "build* capacity" OR "capacity building" OR "capacity development"
      )
      NEAR/5
      ("coping" OR "cope" OR "adapt*" OR "resilien*" OR "mitigat*" OR "preparedness" OR "risk reduction"
      )
    )
    OR
    (
      ("establish*" OR "propose*" OR  "implement*" OR "adopt*" OR "introduc*"
      "roadmap" OR "towards" OR "way to"
      )
      NEAR/5
      (("risk$ ) NEAR/3 ("plan" OR "plans" OR "planning" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "medical response$"))
    )
  )  
  NEAR/15
  (
    (
      ("natural" OR "anthropogenic" OR "environmental" OR "climat*" OR "man-made") 
      NEAR/3 
      ("hazard*" OR "catastroph*" OR "disaster*")
    )
    OR "drought$" OR "flood*" OR "cold spells"
    OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" 
    OR "heatwave$" OR "heat-wave$" OR "wildfire*" OR "forest fire*" OR "wild-fire*" OR "forestfire*" OR 
    OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$"
    OR "landslide$" OR "rockslide$" OR "surface collapse$" OR "mud flow$"
    OR "land-slide$" OR "rock-slide$" OR "mud-flow$"
    OR "tipping point$"  
    OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) OR "tsunami*"
    OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$"))
  )
OR "livelihood vulnerability index"
)

```

## Target 13.2 

> **13.2 Integrate climate change measures into national policies, strategies and planning**
>
>13.2.1 Number of countries with nationally determined contributions, long-term strategies, national adaptation plans and adaptation communications, as reported to the secretariat of the United Nations Framework Convention on Climate Change
>
>13.2.2 Total greenhouse gas emissions per year		

This target is interpreted to cover research about national policies, strategies and planning related to
  - climate change mitigation and adaptation as general topics, inkl. reducing the impacts of indicators of climate change 
  - reduction of greenhouse gases as a fixed class,and six main greenhouse gases (phrase 2)
  - and generel Frameworks for action (phrase 3)

Indicators of climate change are here interpreted as changes that can be observed and measured (https://library.wmo.int/doc_num.php?explnum_id=10618): global mean surface temperature, global ocean heat content, state of ocean acidification, glacier mass balance, Arctic and Antarctic sea-ice extent, global CO2 fraction and global mean sea level

Carbon capture/storage technology can contribute to climate mitigation (i.e. reduction of GHG) but in order to be consistent with our target interpretation method, any papers concerning it must relate the work to climate mitigation or reductions of GHG to be included. The same would apply to reforestation or other mitigation measures. Thus these are not included as individual search terms but assumed to be included in the given phrases.

This query consists of 3 phrases.

##### Phrase 1: 

National policies, strategies and planning related to climate change mitigation and adaptation and similar terms
This phrase does not have an explicit action

``` Ceylon =
TS=
(
  (
    (
      ("climate change$" OR "global warming" OR "climatic change$" OR "changing climate") 
      NEAR/3  
      ("action$" OR "sustainab*" OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*")
    ) 
    OR 
    (
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
    )
  )
  AND
  (("national" OR "state" OR "federal") NEAR/5 ("program*"OR "strateg*"OR "policy" OR "policies" OR "plan" OR "planning" OR "plans")) 
) 
```

##### Phrase 2:
National policies, strategies and planning related to reduction of GHGs = main climate mitigation according to the 2014 IPCC Synthesis Report<sup id="IPCC2014">[3](#f4)</sup> UNEP definition .
The second part of this phrase covers the six main greenhouse gases (covered by the Kyoto Protocol) as listed in the 2014 IPCC Synthesis Report<sup id="IPCC2014">[3](#f4)</sup>. This parts need to be linked to climate change 

Action: reduce 

Basic structure: reduce + greenhouse gas (+ climate change) + national planning
 

``` Ceylon =
TS=
(
  (
    (
    "reduc*" OR "combat*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "alleviat*" OR "tackl*" OR "lower" OR "mitigat*" OR "prevent*" OR "stop*" OR "avoid*"
    )
    NEAR/5
    (
      ("GHG" OR "greenhouse gas" OR "greenhouse gases"
      OR "carbon footprint"
        OR ("climate" NEAR/5 ("human impact$"))
      )
      OR
      ( 
        (
        "methane" OR "CH4" OR "nitrous oxide" OR "N2O" OR "carbon dioxide" OR "CO2" OR "carbon emissions"
        OR "hydrofluorocarbons" OR "HFCs" OR "perfluorocarbons" OR "PFCs" OR "sulphur hexafluoride" OR "sulfur hexafluoride" OR "SF6"
        )
        NEAR/5
        ("climate change$" OR "climatic change$" OR "global warming" OR "changing climate"
        OR (("climate" OR "atmospher*" OR "ocean") NEAR/3 "warming")
        )      
      )
    ) 
  )   
  AND
  ("national"  OR "state" OR "federal") NEAR/5 ("program*"OR "strateg*"OR "policy" OR "policies" OR "plan" OR "planning" OR "plans")) 
)
```

##### Phrase 3:

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

## Target 13.3								

> **13.3 Improve education, awareness-raising and human and institutional capacity on climate change mitigation, adaptation, impact reduction and early warning**
>
>13.3.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

This target is considered to cover research about improving education, general awareness and capacity about climate change mitigation, adaptaion and impact reduction. It also covers technical knowledge transfer, international aid related to this topics. 
Interpretatation of what should be considered as contributing to "human and institutional capacity" is challenging - according to the UNDG definition, it concerns anything that would increase the ability of people and institutions to successfully manage climate change mitigation, adaption, impact reduction and early warning. Here consider we that all research on these topics would contribute, and therefore they do not have to be combined with the concept of capacity.

We include general terms about cimate change mitigation as well as the reduction og greenhouse gases as the main method of climate change mitigation.

This query consists of 1 phrase.

`Green climate fund` is a dedicated climate fund.

##### Phrase 1:


``` Ceylon =
TS=
(
  (
    (
      ("raise" OR "increas*" OR "improv*" OR "enhanc*" OR "build*" OR "develop*" OR "invest" OR "investing") 
      NEAR/5
      ("capacity" OR "technolog*" OR "research" OR "skills" OR "knowledge"  
      OR "tools" OR "awareness" OR "competenc*" "educati*" OR "curriculum" OR "curricula" 
      OR "official development assistance" OR "official development aid" OR       
      "foreign aid" OR "international aid" OR "cooperation fund" )
    )  
    NEAR /15      
    (
      (
        ("climate change$" OR "global warming" OR "climatic change$" OR "changing climate") 
        NEAR/3  
        ("action$" OR "sustainab*" OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*" OR 
        "impact reduction" OR "early warning" OR "risk$")
      )
      OR "climate mitigation" OR "sustainable development"
      OR 
      (
        ("reduc*" OR "combat*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "alleviat*" OR 
        "tackl*" OR "lower" OR "mitigat*" OR "prevent*" OR "stop*" OR "avoid*"
        )
        NEAR/5
        ("GHG" OR "greenhouse gas" OR "greenhouse gases"
        OR "carbon footprint"
        )
      )   
    )
  )  
  OR "green climate fund"
)
        
```
## Target 13.a								

> **13.a Implement the commitment undertaken by developed-country parties to the United Nations Framework Convention on Climate Change to a goal of mobilizing jointly $100 billion annually by 2020 from all sources to address the needs of developing countries in the context of meaningful mitigation actions and transparency on implementation and fully operationalize the Green Climate Fund through its capitalization as soon as possible**
>
>13.a.1 Amounts provided and mobilized in United States dollars per year in relation to the continued existing collective mobilization goal of the $100 billion commitment through to 2025

NO

##### Phrase 1:






## Target 13.b

> **13.b Promote mechanisms for raising capacity for effective climate change-related planning and management in least developed countries and small island developing States, including focusing on women, youth and local and marginalized communities**
>
>13.b.1 Number of least developed countries and small island developing States with nationally determined contributions, long-term strategies, national adaptation plans and adaptation communications, as reported to the secretariat of the United Nations Framework Convention on Climate Change

This target is considered to cover research about planning and management of adaptation to climate change /this is a dificu
https://aurora-network-global.github.io/sdg-queries/query_SDG13.xml

##### Phrase 1: 
Action: raising capacity (OR climate plan)

Basic structure: (raising capacity AND climate action) OR climate planing in LDC or SIDS

TS=
( 
  ( 
    ( 
      ( 
        ("capacity" OR "technolog*" OR "research" OR "skills" OR "knowledge"  
        OR "tools" OR "awareness" OR "competenc*")  
        NEAR/5  
        ("raise" OR "increas*" OR "improv*" OR "enhanc*" OR "build*" OR "develop*" OR "invest" OR "investing") 
      )  
      AND 
      ("climat*"  
  		NEAR/5  
      ("action$" OR "sustainab*" OR "adapt*" OR "cope" OR "coping" OR "resilien*"  
      OR "management" OR "communication") 
      ) 
    )  
    OR  
    ("climat*" NEAR/5 ("strateg*" OR "policy" OR "policies" OR "plan" OR "planning" OR "plans"))
  )   
  AND 
  ("least developed countr*" OR "least developed nation$" OR "small island developing state$" 
  OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Comoros"
  OR "Congo" OR "Djibouti"  OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" 
  OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" 
  OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo"  
  OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" 
  OR "Laos" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" 
  OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "Angola" OR "Benin" OR "Burkina Faso" 
  OR "Burundi" OR "Central African Republic" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" 
  OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" 
  OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" 
  OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR " "Tanzania" OR "Zambia" OR "Cambodia" 
  OR "Kiribati" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR
      "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" 
 ) 

```

## 4. Authorship and review

## 5. Footnotes

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

Old format - I suggest we change to author-date

<b id="f2">2</b> United Nations Development Group (2017) Capacity Development, UNDAF companion guidance. https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance [accessed 19.12.2019] [↩](#UNDGcapacity)

<b id="f3">3</b> IPCC, 2014: Climate Change 2014: Synthesis Report. Contribution of Working Groups I, II and III to the Fifth Assessment Report of the Intergovernmental Panel on Climate Change [Core Writing Team, R.K. Pachauri and L.A. Meyer (eds.)]. IPCC, Geneva, Switzerland, 151 pp. [↩](#IPCC2014)

https://aurora-network-global.github.io/sdg-queries/query_SDG13.xml
