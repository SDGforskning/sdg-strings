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

Terms for improved drinking water sources were found from the indicator 6.1.1 metadata https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf <a href="#f8">(UN Statistics division 2025)</a>.

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

This phrase aims to find research about the use of unsafe drinking water, i.e. drinking water from unimproved water sources or contaminated drinking water. Definitions for unimproved water sources and biological or chemical contaminants of drinking water were found from the indicator metadata 6.1.1. https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf <a href="#f8">(UN Statistics division 2025)</a>.

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

This phrase aims to find research about access to sanitation and hygiene. Terms for the search were found e.g. in the indicator metadata 6.2.1a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf <a href="#f8">(UN Statistics division 2025)</a>.

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

Terms for unimproved sanitation were found from indicator metadata 6.2.1 a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf <a href="#f8">(UN Statistics division 2025)</a>.

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

HLPF review on SDG 6 implementation (2018) <a href="#5">(DESA 2018)</a> states that universal access also implies providing access to services in schools, health-care facilities and other institutional settings. We have not added these as specific terms in the phrases since they are covered by the general syntax 
`access` + `sanitation/hygiene services`.

Terms for removing barriers or facilitating access to sanitation/hygiene services for persons with disabilities were found in <a href="#9">(HLPF 2018)</a>.

Some vulnerable groups of people are mentioned in HPLF review on SDG 6 implementation <a href="#5">("DESA 2018")</a>.

In addition we used UN sources to find terms and groups that can be considered "vulnerable" (Blanchard et al., 2017; Office of the High Commissioner, n.d.; United Nations, n.d.).

* United Nations (n.d.) Fight racism. Vulnerable groups, who are they? <a href="#10">(UN Fight racism)</a>.

* Office of the High Commissioner (n.d.) Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health. United Nations Human Rights. <a href="#11">(Office of the High Commissioner)</a> (accessed Jun 2022). 

* Blanchard et al. (2017). Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment. United Nations Office for Disaster Risk Reduction <a href="#12">(Blanchard)</a>. 

The elements of the phrase are *inequalities OR women/vulnerable groups+access + sanitation/hygiene + services/facilities* 


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
        "*women" OR "*woman" OR "*womens" OR "*womans"
        OR "girl$"
        OR "female$"
        OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
          
        OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"  
        OR "working poor" OR "destitute" OR "living in poverty"
        OR (("poor" OR "poorest" OR "low* income") 
          NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
        OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" 
        OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
        OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
        OR (("person$" OR "people$" OR "adult$" OR "men") 
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
        OR "non-binary" OR "nonbinary" OR "gender non-conforming" OR "gender nonconforming" OR "queer"
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
    ("freshwater" OR "fresh water" OR "lake$" OR "pond$" 
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
  ("freshwater" OR "fresh water" OR "lake$" OR "pond$" 
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
    ("freshwater" OR "fresh water" OR "lake$" OR "pond$" 
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
* UNSD SDG 6 extended report 2022 <a href="#6">(UNSD 2022)</a>
* Indicator metadata 6.4.1 https://unstats.un.org/sdgs/metadata/files/Metadata-06-04-01.pdf <a href="#f8">(UN Statistics division 2025)</a>


The elements of the phrase are *WUE/water security/sustainable withdrawals/water savings*


```py
TS=
( 
  "water use efficiency" OR ("WUE" NEAR/15 "water") 
  OR "water security"  
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
            NEAR/3 ("water" OR "freshwater")
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
      NEAR/3 ("water" OR "freshwater")
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
* Indicator metadata 6.5.1  https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-01.pdf <a href="#f8">(UN Statistics division 2025)</a>
* Indicator metadata 6.5.2 https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-02.pdf <a href="#f8">(UN Statistics division 2025)</a>
* Terms for water management related projects and programmes were found in UNSD SDG 6 Extended report 2022 <a href="#6">(UNSD 2022)</a> and UN-Water pages for Water quality and wastewater <a href="#13">(UN-Water, Water quality & Wastewater)</a>

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
              OR "hydrological unit" OR "watershed"
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
            OR "watershed" 
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

#### Phrase 1 


This phrase aims to find research about protecting freshwater-related ecosystems, their spatial extent and water quality and quantity.

The elements of the phrase are *conserving/protecting + ecosystems/areas/water quality/water quantity + water-related ecosystems*
The structure of the phrase is similar to SDG 14.2 phrase 3.


```py
TS=
(
  ("conserve" OR "conserving" OR "manage" OR "managing" OR "managed" 
  OR "protect" OR "protecting" OR "protected" OR "restore" OR "restoring" OR "rehabilita*"
  OR "management" OR "conservation" OR "protection" OR "restoration" OR "resilien*"
  )
  NEAR/5 
  (
    ("ecosystem$" OR "habitat$" OR "ecological communit*" OR "biotope$" 
    OR ("water" NEAR/3 ("quality" OR "quantity" OR "area" OR "extent" OR "volume")) 
    ) 
      NEAR/5 
       ("freshwater" OR "fresh water" 
        OR "lake*" OR "pond$"
        OR "river*" OR "stream$" OR "brook$" OR "creek$" 
        OR "marsh" OR "marshes" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp$" 
        OR "wetland$" OR "mangrove$" 
        OR "floodplains" OR "rice paddies" 
        OR ("reservoir$" NEAR/3 "water") OR "artificial waterbod*" 
        OR "aquifer$" OR "groundwater"
       )
  )
)
```


#### Phrase 2

This phrase aims to find research about the deterioration of freshwater-related ecosystems.

Terms for deterioration were found in UNSD SDG 6 Extended report 2022 <a href="#6">(UNSD 2022)</a>.

The elements of the phrase are *decline/deterioration/unsustainable use + water-related ecosystems*


```py
TS=
(
  (
  ("deteriorat*" OR "declin*" OR "degrad*" OR "loss" OR "lost" OR "destruct*" OR "disappear*" OR "fragmentat*" 
  OR "erosion" OR "flooding" OR "drought$" 
  OR ("flow" NEAR/3 ("reduced" OR "diminish*" OR "decrased" OR "low*")) 
  OR ("species" NEAR/3 ("extinction" OR "loss")) 
  OR ("biodiversity" NEAR/3 ("loss*" OR "lost"))
  ) 
  OR (
      ("unsustainab*" OR "exploit*") 
        NEAR/5 
        ("manag*" OR "use" OR "using" OR "usage" OR "utili*" OR "govern*" OR "development" OR "administrat*" OR "planning" OR "policy" OR "policies"
        OR ("water" NEAR/3 "extract*"))
      )
  ) 
  NEAR/15 
  (
    ("ecosystem$" OR "habitat$" OR "ecological communit*" OR "biotope$" 
    OR ("water" NEAR/3 ("quality" OR "quantity" OR "area" OR "extent" OR "volume")) 
    ) 
      NEAR/5 
       ("freshwater" OR "fresh water" 
        OR "lake*" OR "pond$"
        OR "river*" OR "stream$" OR "brook$" OR "creek$" 
        OR "marsh" OR "marshes" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp$" 
        OR "wetland$" OR "mangrove$" 
        OR "floodplains" OR "rice paddies" 
        OR ("reservoir$" NEAR/3 "water") OR "artificial waterbod*" 
        OR "aquifer$" OR "groundwater"
       )
  )
)

```


### Target 6.a

> **6.a By 2030, expand international cooperation and capacity-building support to developing countries in water- and sanitation-related activities and programmes, including water harvesting, desalination, water efficiency, wastewater treatment, recycling and reuse technologies**
>
> 6.a.1 Amount of water- and sanitation-related official development assistance that is part of a government-coordinated spending plan

This target is interpreted to cover research about 

#### Phrase 1

The elements of the phrase are *international cooperation/support + capacity building + WASH/drinking water/water harvesting/desalination/water efficiency/wastewater treatment/recycling and reuse of water + developing countries*

```py
TS=
(
  (
    (
      (
      (("international" OR "development") 
        NEAR/3 ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$")) 
      OR "ODA" OR "official development assistance" OR "cooperation fund$" OR "development spending" OR "development aid" OR "development assistance" OR "foreign aid" OR "international aid" OR "international assistance"
      )
      NEAR/15 
        ("institutional capacity" OR "human capacity" OR "technological capacity" OR "scientific capacity" OR "financial capacity" 
        OR "capacity building" OR "capacity development" OR "build* capacity" OR "develop* capacity" 
        OR "infrastructure$" OR "facilities" OR "tools" OR "technical support" OR "managerial support"
        OR "research" OR "knowledge" OR "skills" OR "competenc*" OR "expertise" OR "R&D" OR "innovation" 
        OR "communication" OR "social network$" OR "information network$" OR "campaign$" 
        OR "awareness" OR "disseminat*" OR "educat*" OR "training" 
        OR "knowledge transfer*" OR "transfer of technolog*" OR "technological transfer" OR "technology transfer"
        OR "expenditure" OR "invest" OR "investing" OR "investment$" OR "financing" OR "spending" OR "funding" OR "funder$" OR "fund$" OR "grant$" OR "loan$" OR "microfinance" 
        OR "financial support" OR "financial resources"
        OR "incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e" 
        OR "policy" OR "policies" OR "empower*" OR "strateg*" OR "programme$" OR "program$" OR "intervention$"
        )
      ) 
      NEAR/5 
      (
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
              NEAR/3 ("wastewater" OR "human excret$" OR "faeces" OR "faecal sludge")
          )
          )
            NEAR/5 
            ("sanitation" OR "hygiene" OR "WASH") 
        ) 
      OR 
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

      OR ("water" NEAR/3 ("harvest*" OR "desalinat*")) 
      OR "water use efficiency" OR ("WUE" NEAR/15 "water") 
      OR (("wastewater" OR "waste water" OR "sewage") 
        NEAR/3 ("treatment" OR "recycl*" OR "reuse"))
      ) 
      )
  ) 
AND 
  ("least developed countr*" OR "least developed nation$"
  OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" 
  OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" 
  OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" 
  OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" 
  OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" 
  OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*" 

  OR "small island developing nation$" OR "small-island developing state$" OR "small-island developing countr*"
  OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" 
  OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" 
  OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" 
  OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" 
  OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" 
  OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*"
  OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" 
  OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" 

  OR  "landlocked developing nation$" OR "landlocked developing stat*" OR "land-locked developing nation$" OR "land-locked developing stat*"
  OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" 
  OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" 
  OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" 
  OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" 
  OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*" 

  OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" 
  OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" 
  OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" 
  OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" 
  OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" 
  OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" 
  OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" 
  OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" 
  OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" 
  OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" 
  OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" 
  OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" 
  OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" 
  OR "turkish" OR "turkey" OR "georgia*"
  )
)

```


### Target 6.b

> **6.b Support and strengthen the participation of local communities in improving water and sanitation management**
>
> 6.b.1 Proportion of local administrative units with established and operational policies and procedures for participation of local communities in water and sanitation management

This target is interpreted to cover research about 

#### Phrase 1

The elements of the phrase are *local communities + participation/policies + water and sanitation elements + management*


```py
TS=
(
  (
    ("local" OR "stakeholder$" OR "municip*" OR "communit*" OR "commun*" OR "district") 
    NEAR/5 
      ("participat*" OR "contribut*" OR "impact" OR "plan" OR "planning" 
      OR "choice$" OR "choose" OR "solution$" 
      OR ("decision$" NEAR/3 "making") 
      OR "administrat*" OR "policy" OR "policies" OR "procedure$" OR "scheme$"
      )
  ) 
  NEAR/5 
    (
    ("manage*" OR "develop*" OR "govern*" OR "development" OR "administrat*" OR "plan" OR "planning" OR "policy" OR "policies" OR "extract*" OR "resource us*" OR "usage" 
    OR "consumption" OR "consume$" OR "consumer$" OR "withdrawal$") 
        NEAR/5 
        (
          (("drink*" OR "potable") NEAR/3 "water")
          OR "sanitation" 
          OR ("hygiene" NEAR/3 ("service$" OR "facilit*")) 
          OR "handwashing" OR "hand-washing" OR ("wash*" NEAR/3 "hand$") 
          OR ("WASH" NEAR/3 ("service$" OR "facilit*"))
          OR 
            (
              (
              (("wastewater" OR "waste water" OR "sewage" OR "sewer$") NEAR/3 "treatment") 
              OR ("water" NEAR/3 ("quality" OR "quantity" OR "area" OR "extent" OR "volume")) 
              OR "ecosystem$" OR "habitat$" OR "ecological communit*" OR "biotope$"
              ) 
                NEAR/5 
                  ("freshwater" OR "fresh water" OR "lake$" OR "pond$" 
                  OR "river$" OR ("stream$" NEAR/3 "water") 
                  OR "brook$" OR "creek$" 
                  OR "aquifer$" OR "groundwater" 
                  OR ("water" NEAR/3 "reservoir$"))
            ) 
            OR "water use efficiency" OR ("WUE" NEAR/15 "water") 
            OR "water resource$" OR "freshwater resource$" 
            OR "water supply" OR "water supplies" OR "suppl* of freshwater"
        ) 
    )
)         

```


## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f1">UN DESA. (2025).</span> *Goals: Ensure availability and sustainable management of water and sanitation for all*. https://sdgs.un.org/goals/goal6#targets_and_indicators [Accessed 2025.04.02]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

<span id="f8">UN Statistics Division (2025).</span> *SDG Indicators Metadata Repository*. https://unstats.un.org/sdgs/metadata 

<span id="f3">UN Department of Global Communications (2023).</span> *What Is Goal 6 –Clean Water And Sanitation*. https://www.un.org/sustainabledevelopment/wp-content/uploads/2023/09/Goal-6_Fast-Facts.pdf 

<span id="f4">UN DESA (2023).</span> *HLPF Factsheet SDG 6* https://sdgs.un.org/sites/default/files/2023-07/2023%20HLPF%20Factsheet%20SDG%206.pdf 

<span id="f5">UN DESA (2018).</span> *2018 HLPF Review of SDG implementation: SDG 6 – Ensure availability and sustainable management of water and sanitation for all* https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf 

<span id="f17">High-level Political Forum (2023).</span> *SDGs in focus: SDG 6 and interlinkages with other SDGs – Clean water and sanitation* https://hlpf.un.org/sites/default/files/2023-06/BN%20HLPF%202023%20SDG%206_1.pdf

<span id="f9">HLPF (2018).</span> *Inclusive, Safe, Resilient and Sustainable Societies and Persons with Disabilities: Executive Summary*
https://sdgs.un.org/sites/default/files/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf

<span id="f6">UNSD (2022).</span> *6 Clean Water and Sanitation: The Sustainable Development Goals Extended report 2022* https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf 

<span id="f7">UN-Water.</span> *WASH - Water, Sanitation and Hygiene* https://www.unwater.org/water-facts/wash-water-sanitation-and-hygiene [Accessed 2025.04.28]

UN-Water. *Water and Gender* https://www.unwater.org/water-facts/water-and-gender [Accessed 2025.04.28]

<span id="f13">UN-Water.</span> *Water Quality and Wastewater* https://www.unwater.org/water-facts/water-quality-and-wastewater ("UN-Water Water quality") [Accessed 2025.04.29]

<span id="f14">UN-Water.</span> *Water and Ecosystems* https://www.unwater.org/water-facts/water-and-ecosystems ("UN-Water Ecosystems") [Accessed 2025.04.29]

WHO (2023). *Drinking-water* https://www.who.int/news-room/fact-sheets/detail/drinking-water

<span id="f10">United Nations (n.d.).</span> *Fight racism. Vulnerable groups, who are they?* https://www.un.org/en/fight-racism/vulnerable-groups?gclid=EAIaIQobChMI9ODI_PvC9wIVV53VCh3pQgZCEAAYASAAEgInB_D_BwE (accessed Jun 2022).

<span id="f11">Office of the High Commissioner (n.d.).</span> *Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health*. United Nations Human Rights https://www.ohchr.org/en/special-procedures/sr-health/non-discrimination-groups-vulnerable-situations (accessed Jun 2022).

<span id="f12">Blanchard et al. (2017).</span> *Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment. United Nations Office for Disaster Risk Reduction*. https://www.undrr.org/publication/marginalized-and-minority-groups-consideration-ndra.

<span id="f15"> United Nations Development Group (2017).</span> *Capacity Development UNDAF companion guidance* https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance [accessed 19.12.2019] 

<span id="f16"> UN-Water.</span> *What is water security* https://www.unwater.org/publications/what-water-security-infographic [Accessed 2025.07.10]
