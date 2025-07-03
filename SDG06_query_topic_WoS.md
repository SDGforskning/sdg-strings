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
GENERAL NOTES & NOTES FOR TARGETS
 + SOURCES NOT YET ADDED

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

`Toilets` with synonyms are linked to `adequate` -string to focus on basic services. Term `WC`was not used due to other uses of wc as an abbreviation. `sewege` and `disposal of wastewater` etc. are linked to `sanitation & hygiene` in order to exclude research about wastewater treatment in general.

Term `WASH` is linked to `services or facilities` in order to exclude irrelevant results about wash in other meanings. Term `hygiene`in also linked to `services or facilities` in order to try to focus on services more than consequences of lack of hygiene.

Some of the terms used as action terms in the action approach phrase are lifted in the `availability` string in order to broaden the search.

The elements of the phrase are *access + WASH/safely managed sanitation services*  


```py
TS=
(
  ("access" OR "availab*" OR "unavailab*" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" 
  OR "tackling" OR "tackle" OR "scal* up" OR "upgrad" 
  OR "adequate" OR "safe" OR "improved" OR "basic" OR "equitab*" OR "non-equit*" OR "equal*") 
    NEAR/15 
  (
    "sanitation" 
    OR ("hygiene" NEAR/3 ("service$" OR "facilit*")) 
    OR ("handwashing" OR "hand-washing" OR ("wash*" NEAR/3 "hand$")) 
    OR ("WASH" NEAR/3 ("service$" OR "facilit*"))

    OR "safely managed sanitation services" 
    OR "improved sanitation facilities" 
    OR "wet sanitation technolog*" 
    OR ("flush toilet*" NEAR/3 ("sewer*" OR "septic tank*" OR "pit latrine*")) 
    OR "dry sanitation technologies" 
    OR ("dry pit latrine* with slabs" OR "ventilated pit latrine*" OR "composting toilet*" OR "container based sanitation") 
    OR 
      (
        ("adequate" OR "safe" OR "basic" OR "equitab*" OR "non-equit*") 
          NEAR/5 
            ("toilet*" OR "lavator*" OR "latrine*" OR "water closet*")
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
      NEAR/3 
      (
        ("sanitation" OR "hygiene") NEAR/3 ("service$" OR "facilit*") 
        OR ("handwashing" OR "hand-washing" OR ("wash*" NEAR/3 "hand$")) 
        OR ("WASH" NEAR/3 ("service$" OR "facilit*"))
      )
  )   
  OR "unimproved sanitation facilit*" 
  OR ("flush toilet*" NEAR/3 ("open drain*")) 
  OR "pit latrines without slab*" 
  OR ("open pit*" NEAR/3 ("sanitation" OR "defecation"))
  OR ("hanging" NEAR/3 ("toilet$" OR "latrine$"))
  OR ("unsealed" NEAR/3 ("bucket$" OR "pan$" OR "tray$" OR "container$")) 
  OR "open defecation" 
  OR
      (
      ("bush" OR "ditch" OR "surface water$" OR "channel$" OR "beach*" 
      OR "river$" OR "stream$" OR "sea") 
        NEAR/3 ("defecation")
      ) 
  OR ("contact" NEAR/3 ("human" NEAR/3 ("excret$" OR "faeces" OR "stool" OR "faecal sludge")))
)
```

#### Phrase 3

This phrase aims to find research about inequalities in access to safe sanitation and hygiene services particularly for women, girls and people in vulnerable situations. 

HLPF review on SDG 6 implementation (2018) https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf ("DESA2018") states that universal access also implies providing access to services in schools, health-care facilities and other institutional settings. We have not added these as specific terms in the phrases since they are covered by the general syntax 
`access` + `sanitation/hygiene services`.

Terms for removing barriers or facilitating access to sanitation/hygiene services for persons with disabilities were found in https://sdgs.un.org/sites/default/files/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf
("HLPF2018").

We have defined disadvantaged groups according to https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf ("DESA2018")

In addition we used UN sources to find terms and groups that can be considered "vulnerable" (Blanchard et al., 2017; Office of the High Commissioner, n.d.; United Nations, n.d.).

* United Nations (n.d.) Fight racism. Vulnerable groups, who are they?. https://www.un.org/en/fight-racism/vulnerable-groups?gclid=EAIaIQobChMI9ODI_PvC9wIVV53VCh3pQgZCEAAYASAAEgInB_D_BwE (accessed Jun 2022).("UNracism")

* Office of the High Commissioner (n.d.) Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health. United Nations Human Rights. https://www.ohchr.org/en/special-procedures/sr-health/non-discrimination-groups-vulnerable-situations (accessed Jun 2022). ("NonDiscr")

* Blanchard et al. (2017). Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment. United Nations Office for Disaster Risk Reduction. https://www.undrr.org/publication/marginalized-and-minority-groups-consideration-ndra. ("Blanchard")

The elements of the phrase are *inequalities OR vulnerable groups+access + sanitation/hygiene + services/facilities* 


```py
TS=
(
  (
    (
      "inequalit*" OR "inequity" OR "discriminat*" 
      OR "barrier$" OR "obstacle$" OR "hinder*" OR "hindrance*"
      OR "insecure" OR "dangerous" OR "unsafe" OR "ha?ardous" 
      OR ("narrow" NEAR/3 "entrance*") OR "step$" 
      OR (("lack*" OR "narrow" OR "tight") NEAR/3 "space") OR ("slippery" NEAR/3 "floor$")
      OR "facilitat*" OR "assist*" OR "support*" OR "non$discriminat*"
      OR 
        (
        "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"  
        OR "working poor" OR "destitute" OR "living in poverty"
        OR (("poor" OR "poorest" OR "low* income") 
          NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
        OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" 
        OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
        OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
        OR (("person$" OR "people$" OR "adult$") 
          NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
        OR "disabled" OR "disabilities" OR "disability"
        OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
        OR "unemployed" 
        OR (("work" OR "workplace" OR "worker$" OR "occupational") 
          NEAR/3 ("injury" OR "injuries" OR "illness*" OR "accident$"))
        OR "women" OR "woman" OR "girls" OR "girl"
        OR "pregnant" OR "pregnancy" OR "maternity"
        OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
        OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*" 
        OR "non$binary" 
        OR "living with HIV" OR "living with AIDS"
        OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
        OR "indigenous group$"
        )
    ) 
    NEAR/5 
        ("availab*" OR "access*")
  )
  NEAR/15  
	(
    "sanitation" 
    OR ("hygiene" NEAR/3 ("service$" OR "facilit*")) 
    OR ("handwashing" OR "hand-washing" OR ("wash*" NEAR/3 "hand$")) 
    OR ("WASH" NEAR/3 ("service$" OR "facilit*"))
    OR ("toilet*" OR "lavator*" OR "latrine*" OR "water closet*") 
  )
)
```

### Target 6.3

> **6.3 By 2030, improve water quality by reducing pollution, eliminating dumping and minimizing release of hazardous chemicals and materials, halving the proportion of untreated wastewater and substantially increasing recycling and safe reuse globally**
>
> 6.3.1 Proportion of domestic and industrial wastewater flows safely treated
>
> 6.3.2 Proportion of bodies of water with good ambient water quality

This target is interpreted to cover research about 

#### Phrase 1

This phrase aims to find research about releases of pollution and hazardous chemicals, wastewaters and dumping into fresh water bodies.

In stead of specifying to research about untreated wastewaters we have included research about any wastewaters in freshwater bodies.

This phrase is partly similar to 14.1 phrase 1.

The elements of the phrase are *pollution/wastewater/hazardous chemicals/ + fresh water bodies*


```py
TS=
(
    ("pollut*"
    OR "wastewater" OR "waste water" OR "sewage" OR "sewer$"
    OR "effluent$" 
    OR
    (
      ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "household$" OR "domestic" OR "urban" OR "dumping")
        NEAR/15
          ("waste" OR "discharge" OR "runoff" OR "run off")          
    )
    OR "plastic$" OR "microplastic$" OR "micro plastic$" OR "nanoplastic$" OR "nano plastic$"
    OR
    (
      ("heavy metal$" OR "toxic metal$" OR "mercury" OR "arsenic" OR "cadmium" OR "chromium" OR "copper" OR "nickel" 
      OR "organotin$" OR "tributyltin" OR "TBT" OR "mining" OR "mine tailing$" OR "oil")
        NEAR/15 "contamination"   
    )
    OR "contaminated" OR "contaminant$" OR "toxic chemical$"
    OR "endocrine disrupting chemical$"
    OR "persistent organic pollutant$" OR "pesticide$" OR "herbicide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
    OR "polycyclic aromatic hydrocarbon$" OR "PAH"
    OR "oil spill$" 
    ) 
  AND 
    ("freshwater" OR "lake$" OR "pond$" 
    OR "river$" OR ("stream$" NEAR/3 "water")  
    OR "brook$" OR "creek$" 
    OR "aquifer$" OR "groundwater" 
    OR ("water" NEAR/3 "reservoir$")
    )
)
```

#### Phrase 2

This phrase aims to find research about the treatment, recycling and reuse of wastewaters related to freshwater bodies.

The phrase is partly similar to 14.1 phrase 2.

The elements of the phrase are *action(increase/improve) + treatment/recycling/reuse + wastewaters + freswater bodies*


```py
TS=
(
  (
    ("treatment" OR "recovery"
    OR "technolog*"
    OR "monitor*" OR "assess*"
    OR "indicator$" OR "bioindicator$" OR "index" OR "indices"
    OR "life cycle assess*" OR "LCA"
    OR "environment* assess*" OR "environment* impact assess*"
    OR "manag*" OR "pollution control$"
    OR "strategy" OR "strategies" OR "regulat*" OR "legislat*" OR "policy" OR "policies" OR "framework" OR "programme" 
    OR "recycl*" OR "re-cycl*" OR "reuse$" OR "re-use$" OR "reusing" OR "re-using" 
    ) 
    NEAR/15
        ("pollut*"
        OR "wastewater" OR "waste water" OR "sewage" OR "sewer$"
        OR "effluent$" 
        OR
          (
            ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "household$" OR "domestic" OR "urban" OR "dumping")
            NEAR/15
                ("waste" OR "discharge" OR "runoff" OR "run off")          
          )
        OR "plastic$" OR "microplastic$" OR "micro plastic$" OR "nanoplastic$" OR "nano plastic$"
        OR
          (
            ("heavy metal$" OR "toxic metal$" OR "mercury" OR "arsenic" OR "cadmium" OR "chromium" OR "copper" OR "nickel" 
            OR "organotin$" OR "tributyltin" OR "TBT" OR "mining" OR "mine tailing$" OR "oil"
            )
            NEAR/15 "contamination"   
          )
        OR "contaminated" OR "contaminant$" OR "toxic chemical$"
        OR "endocrine disrupting chemical$"
        OR "persistent organic pollutant$" OR "pesticide$" OR "herbicide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
        OR "polycyclic aromatic hydrocarbon$" OR "PAH"
        OR "oil spill$" 
        ) 
  )
  AND 
  ("freshwater" OR "lake$" OR "pond$" 
  OR "river$" OR ("stream$" NEAR/3 "water") 
  OR "brook$" OR "creek$" 
  OR "aquifer$" OR "groundwater" 
  OR ("water" NEAR/3 "reservoir$"))
)
```

#### Phrase 3

This phrase aims to find research about the water quality of freshwater bodies.

The elements of the phrase are *water quality + freshwater bodies*


```py
TS=
(
  (
  ("quality" NEAR/3 "water") 
  )
    NEAR/15 
    ("freshwater" OR "lake$" OR "pond$" 
    OR "river$" OR ("stream$" NEAR/3 "water") 
    OR "brook$" OR "creek$" 
    OR "aquifer$" OR "groundwater" 
    OR ("water" NEAR/3 "reservoir$"))
)
```

### Target 6.4

> **6.4 By 2030, substantially increase water-use efficiency across all sectors and ensure sustainable withdrawals and supply of freshwater to address water scarcity and substantially reduce the number of people suffering from water scarcity**
>
> 6.4.1 Change in water-use efficiency over time
>
> 6.4.2 Level of water stress: freshwater withdrawal as a proportion of available freshwater resources

This target is interpreted to cover research about 

#### Phrase 1

This phrase aims to find research about water-use efficiency, sustainable withdrawals and water savings.

Terms were found in 
* UNSD SDG 6 extended report 2022 (“UNSDextended2022”)
* Indicator metadata 6.4.1 https://unstats.un.org/sdgs/metadata/files/Metadata-06-04-01.pdf (“UNstats2025”)


The elements of the phrase are *WUE/sustainable withdrawals/water savings*


```py
TS=
( 
  "water use efficiency" OR ("WUE" NEAR/15 "water")  
  OR 
  (
    ("sustainab*" OR "responsib*" OR "environmental*" OR "efficient*") 
      NEAR/3 
    (
      (
        ("extract*" OR "resource us*" OR "usage" OR "consumption" OR "consume$" OR "consumer$" 
            OR "withdrawal$" 
        )
          NEAR/15
            (
            "water supply" OR "water supplies" OR "suppl* of freshwater"
            OR "water resource$" OR "freshwater resource$" 
            )
      )
      OR 
      (
        ("withdrawal$" OR "abstraction" OR "abstracted" OR "allocation") 
            NEAR/3 ("water" OR "fresh$water")
      )
    )
  ) 
  OR 
  (
    ("save" OR "saving$") 
      NEAR/5 
        ("water" NEAR/3 ("withdrawal$" OR "use*"))
  )
) 

```

#### Phrase 2

This phrase aims to find research about the use of water resources, water stress and water scarcity.

The elements of the phrase are *use of water resources/water stress/water scarcity*
A NOT string about was added to exclude irrelevant results about a `water filling algorithm`



```py
TS=
(
(
  (
    (
      ("extract*" OR "resource us*" OR "usage" OR "consumption" OR "consume$" OR "consumer$" 
      OR "withdrawal$" 
      )
        NEAR/15
        (
        "water supply" OR "water supplies" OR "suppl* of freshwater"
        OR "water resource$" OR "freshwater resource$" 
        )
    )
      OR 
    (
    ("withdrawal$" OR "abstraction" OR "abstracted" OR "allocation") 
      NEAR/3 ("water" OR "fresh$water")
    )
  ) 
  OR 
  (
    "water scarcity" OR "water stress" OR "water withdrawal intensity" 
  )
) NOT ("water-filling" OR "water filling") 
)
```

### Target 6.5

> **6.5 By 2030, implement integrated water resources management at all levels, including through transboundary cooperation as appropriate**
>
> 6.5.1 Degree of integrated water resources management
>
> 6.5.2 Proportion of transboundary basin area with an operational arrangement for water cooperation

This query consists of X phrases.



#### Phrase 1

This phrase aims to find research about cross sectoral or co-ordinated water resources management, IWRM or transboundary co-operation.

Terms were found from 
* Indicator metadata 6.5.1  https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-01.pdf ("UNstats2025")
* Indicator metadata 6.5.2 https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-02.pdf.
* Terms for water management related projects and programmes were found in https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf ("UNSDextended2022")

The elements of the phrase are *IWRM/cross-sectoral water management/transboundary co-operation agreements* 


```py
TS=
(
	"integrated water resources management" OR ("IWRM" NEAR/5 "water") 
	OR 
  (
    ("cross sectoral" OR "cross-sectoral" 
    OR"coordinat*" OR "co-ordinat*" OR "integrated" OR "interdependen*") 
      NEAR/5 
        (
          ("manage*" OR "develop*" OR "resource use" OR "usage" OR "withdrawals" 
          OR "govern*" OR "development" OR "administrat*" OR "plan" OR "planning" OR "policy" OR "policies") 
             NEAR/5 
              (
              "water resource$" OR "freshwater resource$" 
              OR "water supply" OR "water supplies" OR "suppl* of freshwater" 
              OR ("water" NEAR/5 "land") 
              OR (("water" OR "river") NEAR/3 "basin") 
              OR "hydrological unit"
              )
        )
  )
	OR 
  (
		(
		("arrangement*" OR "treaty" OR "treaties" OR "agreement*" OR "framework*" 
    OR "convention$" OR "memorandum of understanding")
		    NEAR/5
			  ("co-operation" OR "cooperation" OR "collaboration")
		)
		  NEAR/15 
		    (
		      ("crossboundary" OR "crossborder" OR "cross-boundary" OR "cross-border"
          OR "transboundary" OR "trans-boundary" 
          OR "transborder" OR "trans-border" OR "interstate")
		      NEAR/5
			      ("water basin*" OR "lake*" OR "river*" OR "river basin" OR "stream*" 
            OR "aquifer*" OR "groundwater*" 
            OR "water resource$" OR "freshwater resource$" 
            OR "water supply" OR "water supplies" OR "suppl* of freshwater" 
            OR ("water" NEAR/5 "land") 
            OR (("water" OR "river") NEAR/3 "basin") 
            OR "hydrological unit")
		    )
    )
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
