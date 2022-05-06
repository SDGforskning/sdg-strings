# Search query for SDG13 - Climate Action, Bergen action-approach.

Take urgent action to combat climate change and its impacts.

**Current status**: This string is currently being edited after internal review. It is substantially changed from the original version it was based on (v2019.11). "Full query" not updated.

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

During editing of this string (2021), we have consulted another set of queries for reference: <a id="Aurora">[Aurora Universities network (2020)](#f4)</a>.

## 3.Targets

## Target 13.1

> **13.1 Strengthen resilience and adaptive capacity to climate-related hazards and natural disasters in all countries**
>
>13.1.1 Number of deaths, missing persons and directly affected persons attributed to disasters per 100,000 population
>
>13.1.2 Number of countries that adopt and implement national disaster risk reduction strategies in line with the Sendai Framework for Disaster Risk Reduction 2015–2030
>
>13.1.3 Proportion of local governments that adopt and implement local disaster risk reduction strategies in line with national disaster risk reduction strategies

This target is interpreted to cover research about how to strengthen resilience to climate-related hazards and natural disasters. Strategies dealing with climate-related hazards and natural disasters and how to minimize impact of climate-related hazards and natural disasters are considered to be a method to improve resilience, and improve the indicator 13.1.1.

This query consists of 1 phrase. The basic structure is *action + resilience/impacts/plans + disasters*

The terms for disasters contain both general terms and specific disaster types. We have used the hazards listed in <a id="disasters">[Murray et al., (2021)](#f5)</a> to make a list of disasters based on their classification of hazards into hydrological/meteorological, geohazards, environmental, chemical, biological, technological, and societal. We have included the hydrological and geohazards under "natural" disasters.

``` Ceylon =
TS=
(
  (
    (
      ("improv*" OR "increas*" OR "better" OR "enhanc*" OR "build" OR "strengthen*" OR "raise"
      OR "develop" OR "developing" OR "implement"
      OR "build* capacity" OR "capacity building" OR "capacity development"
      )
      NEAR/5 ("coping" OR "cope" OR "adapt*" OR "resilien*" OR "mitigat*" OR "preparedness" OR "risk reduction")
    )
    OR  
      (
        ("mitigat*" OR "prevent*" OR "reduc*" OR "decreas*" OR "minimis*" OR "minimiz*" OR "manag*")
        NEAR/5 ("impact$" OR "vulnerab*")
      )
    OR
    (
      ("establish*" OR "propos*" OR "implement*" OR "adopt*" OR "introduc*" OR "roadmap" OR "towards" OR "way to")
      NEAR/5
          (
            ("disaster$" OR "risk$")
            NEAR/3
                ("plan" OR "plans" OR "planning" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "program$" OR "programme$" OR "policy" OR "policies" OR "medical response$")
          )
    )
    OR "sendai framework"
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

## Target 13.2

> **13.2 Integrate climate change measures into national policies, strategies and planning**
>
>13.2.1 Number of countries with nationally determined contributions, long-term strategies, national adaptation plans and adaptation communications, as reported to the secretariat of the United Nations Framework Convention on Climate Change
>
>13.2.2 Total greenhouse gas emissions per year		

This target is interpreted to cover research about
  - national policies, strategies and planning related to climate change mitigation and adaptation actions, including  reduction of greenhouse gases (phrase 1)
  - national policies, strategies and planning related to reducing the indicators of climate change & their impacts (phrase 2)
  - national policies, strategies and planning related to international frameworks for action (phrase 3)

Carbon capture/storage technology can contribute to climate mitigation (i.e. reduction of GHG) but in order to be consistent with our  interpretation method, any papers concerning it must relate the work to climate mitigation or reductions of GHG to be included. The same would apply to reforestation or other mitigation measures. Thus these are not included as individual search terms but assumed to be included in the given phrases.

This query consists of 3 phrases.

##### Phrase 1:

This phrase covers national policies, strategies and planning related to climate change mitigation and adaptation. The general structure is *climate change/GHGs + action + national plans + climate*.

We include reduction of greenhouse gases as a mitigation action (national policies, strategies and planning related to reduction of GHGs are one of the main climate mitigation routes according to the 2014 IPCC Synthesis Report (<a id="IPCC2014">[IPCC 2014](#f4)</a>) UNEP definition. We use six main greenhouse gases (covered by the Kyoto Protocol) as search terms (<a id="IPCC2014">[IPCC 2014](#f4)</a>). The final `AND` phrase containing general *climate* terms is necessary as these gases, when used alone with `reduc*`, find some chemical results (e.g. a reaction for methane reduction).

``` Ceylon =
TS=
(
  (
    ("climate change$" OR "global warming" OR "climatic change$" OR "changing climate"
    OR ("warming" NEAR/3 ("climat*" OR "atmospher*" OR "ocean"))
    OR "GHG" OR "greenhouse gas" OR "greenhouse gases"
    OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$"
    OR "methane" OR "CH4" OR "nitrous oxide" OR "N2O" OR "carbon dioxide" OR "CO2" OR "hydrofluorocarbons" OR "HFCs" OR "perfluorocarbons" OR "PFCs" OR "sulphur hexafluoride" OR "sulfur hexafluoride" OR "SF6"
    )
    NEAR/5
          ("action$" OR "sustainab*" OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*"
          OR "reduc*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "lower" OR "mitigat*"
          OR "alleviat*" OR "tackl*" OR "combat*" OR "prevent*" OR "stop*" OR "avoid*"
          )
  )
  AND
    (
      ("national" OR "state" OR "federal" OR "domestic")
      NEAR/5 ("program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans")
    )
  AND
    ("climate" OR "global warming" OR "climatic change$"
    OR ("warming" NEAR/3 ("atmospher*" OR "ocean"))
    OR "GHG" OR "greenhouse gas" OR "greenhouse gases" OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$"
    OR "sea level rise"
    )
)
```

##### Phrase 2:

This phrase covers national policies, strategies and planning related to climate change indicators and their impacts. The general structure is *climate change indicators + action + national plans*.

Indicators of climate change are changes that can be observed and measured (https://library.wmo.int/doc_num.php?explnum_id=10618): global mean surface temperature, global ocean heat content, state of ocean acidification, glacier mass balance, Arctic and Antarctic sea-ice extent, global CO2 fraction and global mean sea level.

``` Ceylon =
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
      ("national" OR "state" OR "federal" OR "domestic")
      NEAR/5 ("program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans")
    )
)
```

##### Phrase 3:

Frameworks for action are included, as documents referencing these are likely to be discussing climate action (i.e. applied climate science rather than basic). This does pick up some results to do with energy transitions, but generally as related to climate.

``` Ceylon =
TS=
(
  ("Kyoto protocol" OR "Paris Agreement"
  OR "COP 21" OR "COP21" OR "COP 22" OR "COP22" OR "COP 23" OR "COP23" OR "COP 24" OR "COP24" OR "COP 25" OR "COP25" OR "COP 26" OR "COP26"
  OR "UNFCCC" OR "United Nations Framework Convention on Climate Change"
  )
    AND
    (
      ("national" OR "state" OR "federal" OR "domestic")
      NEAR/5 ("program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans")
    )
)
```

## Target 13.3								

> **13.3 Improve education, awareness-raising and human and institutional capacity on climate change mitigation, adaptation, impact reduction and early warning**
>
>13.3.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

This target is considered to cover research about improving education, awareness and capacity about climate change mitigation, adaptation,  impact reduction and early warning.

This query consists of 1 phrase. The general structure is *action + education/awareness/capacity + climate mit/adapt/red/warning*

Interpretation of what should be considered as contributing to raising "human and institutional capacity" is challenging - according to the UNDG definition, it concerns anything that would increase the ability of people and institutions to successfully manage the situation. We have interpreted this to include improvements in areas such as technology, infrastructure, research, skills, and knowledge.  
* Definition of "capacity" : "[...] the ability of people, organizations and society as a whole to manage their affairs successfully" (<a id="UNDGcapacity">[United Nations Development Group 2017](#f2)</a>).
* Definition of "capacity development" : "the process whereby people, organizations and society as a whole unleash, strengthen, create, adapt, and maintain capacity over time, in order to achieve development results" (<a id="UNDGcapacity">[United Nations Development Group 2017](#f2)</a>).

For the *climate* terms, we include general terms about climate change mitigation/ adaption/ impact reduction/ early warning as well as the reduction of greenhouse gases (as a main method of climate change mitigation).

In the *action* terms, `increase` is not truncated as there are many works that begin with generic phrases such as "there is an increasing awareness of [research issue]". We include investments as an "action" in the sense that they can drive action (e.g. cooperation fund for education).

We have also included `green climate fund` as a stand-alone term, as the purpose of this fund is improving capacity on climate change ("GCF was established by 194 governments to limit or reduce greenhouse gas (GHG) emissions in developing countries, and to help vulnerable societies adapt to the unavoidable impacts of climate change.", https://www.greenclimate.fund/).

``` Ceylon =
TS=
(
  (
    (
      ("improv*" OR "increase" OR "better" OR "enhanc*" OR "build*" OR "strengthen*" OR "raise"
      OR "develop" OR "developing" OR "create" OR "creation" OR "implement*" OR "integrat*" OR "adopt*"
      OR "invest" OR "investing" OR "development assistance" OR "development aid" OR "development fund*" OR "foreign aid" OR "international aid" OR "cooperation fund*"
      )
      NEAR/5
          ("educat*" OR "curriculum" OR "curricula" OR "teacher training"
          OR "awareness"
          OR "capacity" OR "infrastructure$" OR "technolog*" OR "early warning system$"
          OR "research" OR "knowledge" OR "skills" OR "tools" OR "competenc*"
          )
    )  
  NEAR/15      
      (
        (
          ("climate" OR "global warming" OR "climatic change$" OR "sea level rise")
          NEAR/5  
              ("action$" OR "sustainab*" OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*"
              OR "early warning" OR "preparedness" OR "risk$" OR "vulnerab*"
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
``` Ceylon =
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

<a id="f5"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f3">3</a> IPCC (2014) Climate Change 2014: Synthesis Report. Contribution of Working Groups I, II and III to the Fifth Assessment Report of the Intergovernmental Panel on Climate Change [Core Writing Team, R.K. Pachauri and L.A. Meyer (eds.)]. IPCC, Geneva, Switzerland, 151 pp. [↩](#IPCC2014)

<a id="f5"></a> Murray, V. et al. (2021) Hazard Information Profiles: Supplement to UNDRR-ISC Hazard Definition & Classification Review: Technical Report: Geneva, Switzerland, United Nations Office for Disaster Risk Reduction; Paris, France, International Science Council. (https://council.science/publications/hazard-information-profiles/).[↩](#disasters)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f2">2</a> United Nations Development Group (2017) Capacity Development, UNDAF companion guidance. https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance [accessed 19.12.2019] [↩](#UNDGcapacity)
