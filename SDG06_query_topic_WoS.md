# Search query for SDG 6 - Clean water and sanitation, Bergen topic-approach.

Ensure availability and sustainable management of water and sanitation for all 

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the topics in the SDG 6 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in the SDG 6 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

```
OBS
GENERAL NOTES + SOURCES NOT YET ADDED

```

## 3. Targets

### Target 6.1

> **6.1 By 2030, achieve universal and equitable access to safe and affordable drinking water for all**
>
> 6.1.1 Proportion of population using safely managed drinking water services

This target is interpreted to cover research about access to safe and affordable drinking water for all people. It also includes steps necessary for achieving this, for example `safe management of drinking water services` which is an indicator of this target and `investments in infrastructure`. Some steps, although mentioned in literature (“UNDeptofComm2023”) https://www.un.org/sustainabledevelopment/wp-content/uploads/2023/09/Goal-6_Fast-Facts.pdf   e.g. `protection and restoration of water-related ecosystems` and `hygiene education` are not included in the phrases of this target as they are covered in detail by other targets of SDG 6. 

Together, targets 6.1 and 6.2 form the WASH targets. *The health and socio-economic benefits of safely managed water can only be fully realized alongside safely managed sanitation and good hygiene practices.*  https://www.unwater.org/water-facts/wash-water-sanitation-and-hygiene ("WASH") 

Target 6.1 is related to SDG 11 target 11.1 which is about access to basic services and to target 3.9 about death and illnesses caused e.g. by contaminated water.

#### Phrase 1

This phrase aims to find research about access to drinking water and about safe drinking water services and infrastructures. By the definition of the indicator metadata 6.1.1 safely managed drinking water services refer to using `improved drinking water sources` which are accessible, available when needed and free from contamination. The indicator metadata definitions for accessability and availability would have been difficult to incorporate in the phrase, we have just search for any research mentioning accessable or available drinking water.

Terms for improved drinking water sources were found from the indicator 6.1.1 metadata https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf.  (“UNstats2025”).

The elements of the phrase are *access/availability/affordability/clean/safe + drinking water*

```py
TS=
(
  (
  ("availab*" OR "access" OR "affordab*" OR "clean" OR "safe" OR "improved" OR "manag*" OR "regulat*" OR "quality" OR "monitor*" 
	OR "potable" OR "uncontaminated" OR "unpolluted" OR "pure" 
  OR "piped" OR "tap*" OR "faucet" OR "running" OR "municipal" OR "borehol*" OR "tubewell*" OR "rainwater"
  OR ("protect*" NEAR/3 ("dug well*" OR "spring*")) 
  OR "packaged" OR "delivered" OR "collect*" OR "fetch*" OR "distribut*"
  OR ("water" NEAR/3 "kiosk*")
  ) 
    NEAR/5 
      ("drink*" NEAR/3 "water") 
  ) 
  OR "improved drinking water source*" 
  OR "safely managed drinking water" 
)
```

#### Phrase 2

This phrase aims to find research about the use of unsafe drinking water, i.e. drinking water from unimproved water sources or contaminated drinking water. Definitions for unimproved water sources and biological or chemical contaminants of drinking water were found from the indicator metadata 6.1.1. https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf (“UNstats2025”)

The elements of the phrase are *unsafe/unprotected/contaminated/unimproved sources + drinking water*

```py
TS=
(
  (
    ("unclean" OR "unsafe" OR "impure" OR "unimproved" OR "polluted" OR "contaminated" OR "contamination" 
    OR "unhygienic" OR "unsanitary" OR "insanitary" OR "untreated" 
    OR ("unprotected" NEAR/3 ("dug well*" OR "spring*"))
    OR "surface water*" OR "river*" OR "reservoir*" OR "lake*" OR "pond*" OR "stream*" 
    OR "canal*" OR "channel*" 
    OR (("poor" OR "bad" OR "unknown") NEAR/3 "quality") 
    OR "E. coli" OR "Escherichia coli" OR "coliforms" OR "pathogen*" 
    OR "arsenic" OR "fluoride*" 
    )
       
      NEAR/5 
      ("drink*" NEAR/3 "water")
  )
  OR "unimproved drinking water source*" 
)
```

### Target 6.2

> **6.2 By 2030, achieve access to adequate and equitable sanitation and hygiene for all and end open defecation, paying special attention to the needs of women and girls and those in vulnerable situations**
>
> 6.2.1 Proportion of population using (a) safely managed sanitation services and (b) a hand-washing facility with soap and water

This target is interpreted to cover research about 


Target 6.2 is related to SDG 11 target 11.1 which is about access to basic services.

#### Phrase 1

This phrase aims to find research about access to sanitation and hygiene. Terms for the search were found e.g. in the indicator metadata 6.2.1a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (UNstats2025).

`Toilets` with synonyms are linked to `adequate` -string to focus on basic services. And `sewege` and `disposal of wastewater` etc. are linked to `sanitation & hygiene` in order to exclude research about wastewater treatment in general.

Term `WASH` is linked to `services or facilities` in order to exclude irrelevant results about wash in other meanings.

Some of the terms used as action terms in the action approach phrase are lifted in the `availability` string in order to broaden the search.

The elements of the phrase are *access + WASH/safely managed sanitation services*  


```py
TS=
(("availab*" OR "unavailab*" OR "access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" 
OR "tackling" OR "tackle" OR "scal* up" OR "upgrad") 
  NEAR/15 
(
    ("sanitation" OR "hygiene" OR "handwashing" OR "hand-washing" OR ("wash*" NEAR/3 "hand$") 
    OR ("WASH" NEAR/3 ("service$" OR "facilit*"))
    )  

    OR "safely managed sanitation services" 
    OR "improved sanitation facilities" 
    OR "wet sanitation technolog*" 
    OR ("flush toilet*" NEAR/3 ("sewer*" OR "septic tank*" OR "pit latrine*")) 
    OR "dry sanitation technologies" 
    OR ("dry pit latrine* with slabs" OR "ventilated pit latrine*" OR "composting toilet*" OR "container based sanitation") 
    OR 
      (
        ("adequate" OR "safe" OR "improved" OR "basic" OR "equitab*" OR "non-equit*") 
          NEAR/5 
            ("toilet*" OR "lavator*" OR "latrine*" OR "WC" OR "water closet*")
      ) 
      OR 
      (
        ("sewege" 
          OR
          (
          ("dispos*" OR "removal" OR "remove*" OR "treat*" OR "containment" 
          OR "emptying" OR "transport" OR "reuse") 
              NEAR/3 ("wastewater" OR "human excreta" OR "faecal sludge")
          )
        )
            NEAR/5 
            ("sanitation" OR "hygiene" OR "WASH") 
      )
)
)       

```

#### Phrase 2

This phrase aims to find research about the lack of sanitation or unsafe i.e. unimproved sanitation such as practicing open defecation as well as lack of hygiene services.

Terms for unimproved sanitation were found from indicator metadata 6.2.1 a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (“UNstats2025”)

The elements of the phrase are *inadequate/unsafe/unimproved/lacking + sanitation/hygiene + service/facility*


```py
TS=
(
  (
    ("inadequate" OR "unsafe" OR "poor" OR "bad" OR "unknown" OR "lack*" OR "unimproved" OR "unsafe" 
    OR "absent" OR "absence" OR "unhygienic" OR "unsanitary" OR "insanitary") 
      NEAR/3 (("sanitation" OR "hygiene") NEAR/3 ("service$" OR "facilit*"))
  )   
  OR "unimproved sanitation facilit*" 
  OR ("flush toilet*" NEAR/3 ("open drain*")) 
  OR "pit latrines without slab*" 
  OR ("open pit*" NEAR/3 ("sanitation" OR "defecation"))
  OR ("hanging" NEAR/3 ("toilet$" OR "latrine$"))
  OR ("unsealed" NEAR/3 ("bucket$" OR "pan$" OR "tray$" OR "container$")) 
  OR "defecation area$" OR "area$ of defecation" 
  OR
      (
      ("bush" OR "ditch" OR "surface water$" OR "channel$" OR "beach*" 
      OR "river$" OR "stream$" OR "sea") 
        NEAR/3 ("defecation")
      ) 
  OR ("contact" NEAR/3 ("human" NEAR/3 ("excret$" OR "faeces" OR "stool" OR "faecal sludge")))
)
```

### Target 6.3

> **6.3 By 2030, improve water quality by reducing pollution, eliminating dumping and minimizing release of hazardous chemicals and materials, halving the proportion of untreated wastewater and substantially increasing recycling and safe reuse globally**
>
> 6.3.1 Proportion of domestic and industrial wastewater flows safely treated
>
> 6.3.2 Proportion of bodies of water with good ambient water quality

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 6.4

> **6.4 By 2030, substantially increase water-use efficiency across all sectors and ensure sustainable withdrawals and supply of freshwater to address water scarcity and substantially reduce the number of people suffering from water scarcity**
>
> 6.4.1 Change in water-use efficiency over time
>
> 6.4.2 Level of water stress: freshwater withdrawal as a proportion of available freshwater resources

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 6.5

> **6.5 By 2030, implement integrated water resources management at all levels, including through transboundary cooperation as appropriate**
>
> 6.5.1 Degree of integrated water resources management
>
> 6.5.2 Proportion of transboundary basin area with an operational arrangement for water cooperation

This query consists of X phrases.

```py
TS=
(

)
```

### Target 6.6

> **6.6 By 2020, protect and restore water-related ecosystems, including mountains, forests, wetlands, rivers, aquifers and lakes**
>
> 6.6.1 Change in the extent of water-related ecosystems over time

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 6.a

> **6.a By 2030, expand international cooperation and capacity-building support to developing countries in water- and sanitation-related activities and programmes, including water harvesting, desalination, water efficiency, wastewater treatment, recycling and reuse technologies**
>
> 6.a.1 Amount of water- and sanitation-related official development assistance that is part of a government-coordinated spending plan

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 6.b

> **6.b Support and strengthen the participation of local communities in improving water and sanitation management**
>
> 6.b.1 Proportion of local administrative units with established and operational policies and procedures for participation of local communities in water and sanitation management

This target is interpreted to cover research about 

```py
TS=
(

)
```


## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f1">UN DESA. (2025).</span> *Goals: Ensure availability and sustainable management of water and sanitation for all*. https://sdgs.un.org/goals/goal6#targets_and_indicators [Accessed 2025.04.02]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/
