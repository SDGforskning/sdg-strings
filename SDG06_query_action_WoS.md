# Search query for SDG 6 - Clean water and sanitation, Bergen action-approach.

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

This document contains search strings for finding publications related to the actions in the SDG 6 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 6 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

For general definitions and finding terms for several targets we used
* UN Department of Global Communications (2023). What Is Goal 6 –Clean Water And Sanitation https://www.un.org/sustainabledevelopment/wp-content/uploads/2023/09/Goal-6_Fast-Facts.pdf ("UNDeptofComm2023")
* UN DESA (2023). HLPF Factsheet SDG 6 https://sdgs.un.org/sites/default/files/2023-07/2023%20HLPF%20Factsheet%20SDG%206.pdf ("DESAfact2023")
* UN DESA/DSDG et al. (2018). 2018 HLPF Review of SDG implementation: SDG 6 – Ensure availability and sustainable management of water and sanitation for all https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf   
("DESA2018")
* UNSD (2022). 6 Clean Water and Sanitation: The Sustainable Development Goals Extended report 2022 https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf ("UNSDextended2022")
* UN-Water website’s Water fact pages https://www.unwater.org/water-facts




## 3. Targets

### Target 6.1

> **6.1 By 2030, achieve universal and equitable access to safe and affordable drinking water for all**
>
> 6.1.1 Proportion of population using safely managed drinking water services

This target is interpreted to cover research about advancing access to safe and affordable drinking water for all people. It also includes steps necessary for achieving this, for example `safe management of drinking water services` which is an indicator of this target and `investments in infrastructure`. Some steps, although mentioned in literature (“UNDeptofComm2023”) https://www.un.org/sustainabledevelopment/wp-content/uploads/2023/09/Goal-6_Fast-Facts.pdf   e.g. `protection and restoration of water-related ecosystems` and `hygiene education` are not included in the phrases of this target as they are covered in detail by other targets of SDG 6. 

Together, targets 6.1 and 6.2 form the WASH targets. *The health and socio-economic benefits of safely managed water can only be fully realized alongside safely managed sanitation and good hygiene practices.*  https://www.unwater.org/water-facts/wash-water-sanitation-and-hygiene ("WASH") 

Target 6.1 is related to SDG 11 target 11.1 which is about access to basic services and to target 3.9 about death and illnesses caused e.g. by contaminated water.


#### Phrase 1

This phrase aims to find research about advancing access to safe and affordable drinking water and about promoting and investing in safely managed drinking water services and infrastructures. By the definition of the indicator metadata 6.1.1 safely managed drinking water services refer to using `improved drinking water sources` which are accessible, available when needed and free from contamination. The indicator metadata definitions for accessability and availability would have been difficult to incorporate in the phrase, we have just search for any research mentioning accessable or available drinking water.

Terms for improved drinking water sources were found from the indicator 6.1.1 metadata https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf.  (“UNstats2025”).

The elements of the phrase are *action + access/availability/affordability/management/regulation/investment + safe/improved + drinking water*

```py
TS=
(
  (
    (
      ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher"
      OR "overcome" OR "ensure" OR "attain*" OR "achiev*"OR "upgrad*" 
      OR "tackling" OR "tackle"
      OR "scal* up" OR "expand" OR "expansion*" OR "advance" OR "advancing" OR "develop" OR "developing"
      OR "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limiting" OR "limited" 
      OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*"
      )
        NEAR/5
          ("availab*" OR "access" OR "affordab*" OR "management" OR "regulat*" OR "invest*" 
          OR "obstacle$" OR "barrier$" OR "hinder*" OR "hindrance*")
    )
    OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*" OR "project*" OR "intervention*"
  )
    NEAR/15 
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
)
```

#### Phrase 2

This phrase aims to find research about reducing the use of unsafe drinking water, i.e. drinking water from unimproved water sources or contaminated drinking water. Definitions for unimproved water sources and biological or chemical contaminants of drinking water were found from the indicator metadata 6.1.1. https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf (“UNstats2025”)

The elements of the phrase are *action + unsafe/unprotected/contaminated/unimproved sources + drinking water*

```py
TS=
(
  (
    "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limiting" OR "limited" 
    OR "stop" OR "end" OR "ending" 
    OR "tackling" OR "tackle"
    OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*" OR"overcome" 
    OR "ensure" OR "attain*" OR "achiev*"OR "upgrad*"
    OR "scal* up" OR "develop" OR "developing"
    OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" 
    OR "program*" OR "project*"  
  )
    NEAR/15 
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
)
```


### Target 6.2

> **6.2 By 2030, achieve access to adequate and equitable sanitation and hygiene for all and end open defecation, paying special attention to the needs of women and girls and those in vulnerable situations**
>
> 6.2.1 Proportion of population using (a) safely managed sanitation services and (b) a hand-washing facility with soap and water

This target is interpreted to cover research about advancing access to adequate and equitable sanitation and hygiene for all people and in particular women and girls and people in vulnerable situations. It is also about abandoning unimproved sanitation facilities or lack of sanitation i.e. practicing open defecation. https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf (”DESA2018”).

What is adequate sanitation? According to the definitions of the indicator metadata 6.2.1a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (“UNstats2025”) 

> *Safely managed sanitation services is about using improved sanitation facilities*.
> 
> *Use of improved sanitation facilities which are not shared is defined as a basic sanitation service.
> While the use of shared improved  sanitation facilities is defined as limited sanitation service*.
> 
> *Safely managed sanitation services also refer to facilities where the excreta are safely disposed of in situ or removed
> and treated off-site and hygienically separate from human contact*.

However, in addition to searching for safely managed sanitation services as defined in the indicator metadata 6.2.1a we have built the phrases to search for any research mentioning advancing access to sanitation as we interpreted this to be aim of the target and would have lost relevant research by restricting to research mentioning "adequate".

We were unsure whether oral hygiene should be included as it is not specifically mentioned in the background materials. Currently, the phrases do not excluded it.

Target 6.2 is related to SDG 11 target 11.1 which is about access to safe housing and basic services.

As the target is about equal access and a particular focus is on women, girls and people in vulnerable situations we interpret this target also to include eliminating inequalities they may face in access to sanitation and hygiene. 


#### Phrase 1

This phrase aims to find research about providing access to sanitation and hygiene for all people. Terms for the search were found e.g. in the indicator metadata 6.2.1a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (UNstats2025).

`Toilets` with synonyms are linked to `adequate` -string to focus on basic services. Term `WC`was not used due to other uses of wc as an abbreviation. `sewege` and `disposal of wastewater` etc. are linked to `sanitation & hygiene` in order to exclude research about wastewater treatment in general.

Term `WASH` is linked to `services or facilities` in order to exclude irrelevant results about wash in other meanings. Term `hygiene`in also linked to `services or facilities` in order to try to focus on services more than consequences of lack of hygiene.

The elements of the phrase are *action + access + WASH/safely managed sanitation services*  


```py
TS=
(
  (
    (
       ( "increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher"
        OR "overcome" OR "ensure" OR "attain*" OR "achiev*"OR "upgrad*" 
        OR "tackling" OR "tackle"  
        OR "scal* up" OR "expand" OR "expansion*" OR "advance" OR "advancing" OR "develop" OR "developing"
        OR "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limiting" OR "limited" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR 	"combat*" OR "declin*"
       ) 
       NEAR/5
            ("availab*" OR "access" OR "obstacle$" OR "barrier$" OR "hinder*" OR "hindrance*" 
            OR "safe" OR "improved" OR "basic" OR "equitab*" OR "non-equit*" OR "equal*")
    )
    OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*" OR "project*" OR "intervention*"
  )
   
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
              NEAR/3 ("wastewater" OR "human excret$" OR "faeces" OR "faecal sludge")
          )
        )
            NEAR/5 
            ("sanitation" OR "hygiene" OR "WASH") 
      )
  )
)        
```

#### Phrase 2

This phrase aims to find research about abandoning lack of sanitation or unsafe i.e. unimproved sanitation such as practicing open defecation as well as lack of hygiene services.

Terms for unimproved sanitation were found from indicator metadata 6.2.1 a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (“UNstats2025”)

The elements of the phrase are *action + inadequate/unsafe/unimproved/lacking + sanitation/hygiene + service/facility*


```py
TS=
(
  (
    "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limiting" OR "limited" 
    OR "stop" OR "end" OR "ending" OR "abandon" 
    OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*" OR"overcome" 
    OR "ensure" OR "attain*" OR "achiev*"OR "upgrad*"
    OR "scal* up" OR "develop" OR "developing"
    OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" 
    OR "program*" OR "project*"  
  )
    NEAR/15 
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
)
```

#### Phrase 3

This phrase aims to find research about eliminating inequalities in access to safe sanitation and hygiene services particularly for women, girls and people in vulnerable situations. 

HLPF review on SDG 6 implementation (2018) https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf ("DESA2018") states that universal access also implies providing access to services in schools, health-care facilities and other institutional settings. We have not added these as specific terms in the phrases since they are covered by the general syntax 
`access` + `sanitation/hygiene services`.

Terms for removing barriers or facilitating access to sanitation/hygiene services for persons with disabilities were found in https://sdgs.un.org/sites/default/files/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf
("HLPF2018").

We have defined disadvantaged groups according to https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf ("DESA2018")

In addition we used UN sources to find terms and groups that can be considered "vulnerable" (Blanchard et al., 2017; Office of the High Commissioner, n.d.; United Nations, n.d.).

* United Nations (n.d.) Fight racism. Vulnerable groups, who are they?. https://www.un.org/en/fight-racism/vulnerable-groups?gclid=EAIaIQobChMI9ODI_PvC9wIVV53VCh3pQgZCEAAYASAAEgInB_D_BwE (accessed Jun 2022).("UNracism")

* Office of the High Commissioner (n.d.) Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health. United Nations Human Rights. https://www.ohchr.org/en/special-procedures/sr-health/non-discrimination-groups-vulnerable-situations (accessed Jun 2022). ("NonDiscr")

* Blanchard et al. (2017). Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment. United Nations Office for Disaster Risk Reduction. https://www.undrr.org/publication/marginalized-and-minority-groups-consideration-ndra. ("Blanchard")

The elements of the phrase are *action(eliminate OR facilitate) + inequalities OR vulnerable groups+access + sanitation/hygiene + services/facilities* 


```py
TS=
(
  (
    (
      ("eliminat*" OR "remov*") 
      NEAR/5 
        (
        ("inequalit*" OR "inequity" OR "discriminat*" 
        OR "barrier$" OR "obstacle$" OR "hinder*" OR "hindrance*"
        OR "insecure" OR "dangerous" OR "unsafe" OR "ha?ardous") 
        OR ("narrow" NEAR/3 "entrance*") OR "step$" 
        OR (("lack*" OR "narrow" OR "tight") NEAR/3 "space") OR ("slippery" NEAR/3 "floor$")
        ) 
    )
  OR
    (
      ("facilitat*" OR "assist*" OR "support*" OR "non$discriminat*" 
        OR 
        ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"  
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
https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf (“UNSDextended2022”); https://www.unwater.org/water-facts/water-quality-and-wastewater ("WASTE")
* improving water quality
* reducing the proportion of untreated wastewaters discharged into the environment and releases of pollution and hazardous chemicals and materials
* increasing recycling and safe reuse of water
* monitoring of water quality

Althoug mentioned in the background materials, terms `nutrients` and `fertilizers` were not included in the phrases in order to not focus too much in the ecology/biology of freswater body species. We interpreted this target to be more about the water quality.

This target focuses on freshwater bodies. The ones mentioned in the 6.3.2 indicator metadata are `lakes` `rivers` `streams` `groundwaters` `aquifers`  `reservoirs` . Term `stream` is combined with `water` in order to exclude irrelevant results e.g. about waste stream.

The classification for wastewater generators is https://unstats.un.org/sdgs/metadata/files/Metadata-06-03-02.pdf (“UNstats2025)
* domestic/households
* industrial
* services

Runoff from urban and agricultural land is counted as wastewater but not monitored systematically
https://unstats.un.org/sdgs/metadata/files/Metadata-06-03-01.pdf (“UNstats2025)

Target 6.3 is related to targets 
* SDG 14.1 preventing and reducing marine pollution
* SDG 12.4 reducing harmful releases to water
* SDG 12.5 reducing waste through e.g. recycling and reuse

#### Phrase 1

This phrase aims to find research about reducing or eliminating releases of pollution and hazardous chemicals, wastewaters and dumping into fresh water bodies.

In stead of specifying to research about reducing untreated wastewaters we have included research about reducing any wastewaters in freshwater bodies.

This phrase is partly similar to 14.1 phrase 1.

The elements of the phrase are *action + pollution/wastewater/hazardous chemicals/ + fresh water bodies*


```py
TS=
(
  (
    ("prevent*" OR "avoid*" OR "stop*" OR "remov*" OR "eliminat*" OR "combat" OR "fight"
    OR "minimi*" OR "restrict*" OR "mitigat*" OR "alleviat*" OR "reduc*" OR "decreas*"
    OR "prohibit*" OR "protect*"
    OR "remediate" OR "remediation" OR "cleanup" OR "clean up"
    )  
    NEAR/5
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

#### Phrase 2

This phrase aims to find research about increasing or improving treatment, recycling and reuse of wastewaters related to freshwater bodies.

The phrase is partly similar to 14.1 phrase 2.

The elements of the phrase are *action(increase/improve) + treatment/recycling/reuse + wastewaters + freswater bodies*


```py
TS=
(
  (
    (
        ("improv*" OR "strengthen*" OR "enhanc*" OR "scal* up" OR "upgrad*"
        OR "develop" OR "developing" OR "implement*" OR "establish*" OR "build*" OR "propose*" OR "introduce" OR "design*" OR "adopt*"
        OR "enforc*" OR "prioriti*"
        )
        NEAR/5
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

This phrase aims to find research about increasing, improving and monitoring water quality of  freshwater bodies.

The elements of the phrase are *action(increase/improve/monitor) + water quality + freshwater bodies*


```py
TS=
(
("incres*" OR "improv*" OR "strengthen*" OR "enhanc*" OR "scal* up" OR "upgrad*"
OR "develop" OR "developing" OR "implement*" OR "establish*" OR "build*" OR "propose*" OR "introduce" OR "design*" OR "adopt*"
OR "enforc*" OR "prioriti*" 
OR "monitor*"
)
  NEAR/5 
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
)
```


### Target 6.4

> **6.4 By 2030, substantially increase water-use efficiency across all sectors and ensure sustainable withdrawals and supply of freshwater to address water scarcity and substantially reduce the number of people suffering from water scarcity**
>
> 6.4.1 Change in water-use efficiency over time
>
> 6.4.2 Level of water stress: freshwater withdrawal as a proportion of available freshwater resources

This target is interpreted to cover research about increasing water-use efficiency (WUE) and ensuring that freshwater withdrawals are sustainable on all sectors. It is about reducing water scarcity and levels of water stress and ensuring a sustainable supply of freshwater.

By the definition of the indicator metadata 6.4.1 https://unstats.un.org/sdgs/metadata/files/Metadata-06-04-01.pdf (“UNstats2025”)

> **Water use efficiency (WUE**) is
> *The value added of a given sector divided by the volume of water used*.
>
> **The sectors** included are
> * Agriculture (ISIC A): 
> 	Agriculture; foresty; fishing
> 
> * Industry (MIMEC) (ISIC B, C, D and F): 
> 	Mining; quarrying; manufacturing; 
> 	electricity, gas, steam and air conditioning supply; 
> 	constructions; 
> 	cooling of thermoelectric plants
> 
> * Service sectors (ISIC E, ISIC G-T)
	Which includes e.g. water used primarily for the direct use of population

Although sectors are specified in the sources we have not specified sectors in the phrases. The phrases are searching for any research about sustainable use of water supplies. Also, we have not made efforts to exclude withdrawals of non-conventional water, i.e. `treated wastewater` `agricultural drainage water` or `desalinated water`although these were mentioned as not-included in the indicator metadata 6.4.2 https://unstats.un.org/sdgs/metadata/files/Metadata-06-04-02.pdf (“UNstats2025”)

We are unsure about whether research about water efficiency of agricultural plants should be considered relevant to this topic. Since HLPF 2018 ("DESA2018") mentiones agricultural sector as the largest user of fresh water and names e.g. increasing productivity of food crops and growing fewer water-intensive crops as means to water savings we have not tried to exclude these from the results.

#### Phrase 1

This phrase aims to find research about promoting water-use efficiency, sustainable withdrawals and water savings as well as reducing inefficient water-use or unsustainable withdrawals.

Terms were found in 
* UNSD SDG 6 extended report 2022 (“UNSDextended2022”)
* Indicator metadata 6.4.1 https://unstats.un.org/sdgs/metadata/files/Metadata-06-04-01.pdf (“UNstats2025”)


The elements of the phrase are *action(increase/decrease) + WUE/sustainable withdrawals/water savings*


```py
TS=
( 
  ("promote" OR "enable" OR "increase" OR "establish*" OR "develop" OR "development"
  OR "propose*" OR "proposal$" OR "implement*" OR "prioriti?e" 
  OR "ensur*" OR "assure" OR "strengthen" OR "improv*" OR "advance" 
  OR "reduc*" OR "decreas*" OR "minimi*" OR "combat*" OR "resist*" OR "avoid*" 
  OR "tackle" OR "tackling"
  ) 
  NEAR/5 
  ( 
    "water use efficiency" OR ("WUE" NEAR/15 "water") 
    OR 
    (
      ("sustainab*" OR "responsib*" OR "environmental*" OR "efficient*" 
      OR "unsustainab*" OR "irresponsib*" OR "inefficient*") 
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
)    


```


#### Phrase 2

This phrase aims to find research about reducing the use of water resources, water stress and water scarcity.

The elements of the phrase are *action + use of water resources/water stress/water scarcity*
A NOT string about was added to exclude irrelevant results about a `water filling algorithm`

```py
TS=
(
(
  ("reduc*" OR "decreas*" OR "minimi*" OR "combat*" OR "resist*" OR "avoid*") 
    NEAR/5 
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

This target is interpreted to cover research about implementing water resource management, in particular integrated water resources management (IWRM) and transboundary co-operation in water resources management. 

**Integrated water resources management (IWRM)** is based on an internationally agreed definition https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-01.pdf ("UNstats2025"). It is a cross-sectoral approach to water resources management based on the interdependence of uses of water resources on different sectors. It consists of various dimensions including enabling environment (policies, laws, etc), roles of supporting institutions, management instruments for choices between alternative actions and financing.
> *Integrated Water Resources Management (IWRM) promotes the coordinated development and management of water, land and related resources to
>  maximize economic and social welfare in an equitable manner, without compromising the sustainability of vital ecosystems*.

Transboundary co-operation refers to operational agreements on water management between countries sharing transboundary rivers, lakes and aquifers. 



#### Phrase 1

This phrase aims to find research about implementing cross sectoral or co-ordinated water resources management, IWRM or transboundary co-operation.

Terms were found from 
* Indicator metadata 6.5.1  https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-01.pdf ("UNstats2025")
* Indicator metadata 6.5.2 https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-02.pdf.
* Terms for water management related projects and programmes were found in https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf ("UNSDextended2022")

The elements of the phrase are *action(implement/advance) + IWRM/cross-sectoral water management/transboundary co-operation agreements* 


```py
TS=
(
  ("implement*" OR "advanc*" OR "promot*" OR "enhanc*"
  OR "establish*" OR "develop" OR "development"
  OR "propose*" OR "proposal$") 
NEAR/5 
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
)
```

### Target 6.6

> **6.6 By 2020, protect and restore water-related ecosystems, including mountains, forests, wetlands, rivers, aquifers and lakes**
>
> 6.6.1 Change in the extent of water-related ecosystems over time

This target is interpreted to cover research about protecting and restoring water-related ecosystems.

It focuses on protecting freshwater resources containing ecosystems, the spatial area of them and the quality and quantity of water in them. https://www.unwater.org/water-facts/water-and-ecosystems ("ECO")

By the definition of indicator metadata 6.6.1a  https://unstats.un.org/sdgs/metadata/files/Metadata-06-06-01a.pdf (“UNstats2025”)
Included in water-related ecosystems are `lakes` `rivers` `streams` `groundwater` `artificial waterbodies` and `wetlands`   
Wetlands include  `marshes` `peatland` `swamps` `bogs` `fens` `floodplains` `rice paddies` `flood recession agriculture`  
Also `mangroves` are included here although they contain brackish water instead of fresh. 

This target is related to
* SDG 15, particularly to target 15.1 about conservation of terrestrial and freshwater ecosystems
  
However, we interpret target 6.6 to be more focused on the protection of freshwater supplies than in the protection of species. 

Although indicator metadata 6.6.1a excludes mountain and forest ecosystems we have not filtered them from the results since the water-related ecosystems of mountains and forests are perticularly mentioned in the title of this target.

#### Phrase 1 


This phrase aims to find research about protecting freshwater-related ecosystems, their spatial extent and water quality and quantity.

The elements of the phrase are *action + conservation + ecosystems/areas/water quality/water quantity + water-related ecosystems* 
The structure of the phrase is similar to SDG 14.2 phrase 3.


```py
TS=
(
  ("conserve" OR "manage" OR "protect" OR "restore" OR "rehabilitate"
  OR
    (
      ("designat*" OR "placement" OR "expand*" OR "extend"
      OR "design" OR "designing" OR "create" OR "creation" OR "creating"
      OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e"
      OR "plans" OR "plan" OR "planned" OR "planning" OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "strategy" OR "governance"
      OR "enforce" OR "enforcement" OR "enforcing"
      OR "increas*" OR "strengthen" OR "improv*" OR "enhance" OR "facilitat*"
      OR "preserv*" OR "support*" OR "ensur*"
      )
      NEAR/5
        ("conservation" OR "management" OR "protection" OR "restoration" OR "rehabilitation" OR "sustainable" OR "resilien*")
    )
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

This phrase aims to find research about preventing the deterioration of freshwater-related ecosystems.

Terms for deterioration were found in UNSD SDG 6 Extended report 2022 https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf (“UNSDextended2022”)

The elements of the phrase are *action + decline/deterioration/unsustainable use + water-related ecosystems*


```py
TS=
(
("prevent" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "avoid*" OR "combat*" OR "halt*" OR "resist*" OR "minimi*" OR "avoid*" OR "tackle") 
  NEAR/5 
  (
    (
    ("deteriorat*" OR "declin*" OR "degrad*" OR "loss" OR "lost" OR "destruct*" OR "disappear*" OR "fragmentat*"
    OR "erosion" OR "flooding" OR "drought$" 
    OR ("flow" NEAR/3 ("reduced" OR "diminish*" OR "decrased" OR "low*")) 
    OR ("species" NEAR/3 ("extinction" OR "loss")) 
    OR ("biodiversity" NEAR/3 ("loss*" OR "lost"))) 
    OR (
        ("unsustainab*" OR "exploit*") 
        NEAR/5 
          ("manag*" OR "use" OR "using" OR "usage" OR "utili*" OR "govern*" OR "development" OR "administrat*" OR "planning" OR "policy" OR "policies")
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
)

```




### Target 6.a

> **6.a By 2030, expand international cooperation and capacity-building support to developing countries in water- and sanitation-related activities and programmes, including water harvesting, desalination, water efficiency, wastewater treatment, recycling and reuse technologies**
>
> 6.a.1 Amount of water- and sanitation-related official development assistance that is part of a government-coordinated spending plan

This target is interpreted to cover research about expanding international co-operation and capacity-building to support developing countries in WASH related activities and programmes. Activities specifically mentioned are `water harvesting` `desalination` `water efficiency` `wastewater treatment` `recycling and reuse`

As definition of capacity building we have used
* Definition of "capacity development": "the process whereby people, organizations and society as a whole unleash, strengthen, create, adapt, and maintain capacity over time, in order to achieve development results" (United Nations Development Group 2017).
United Nations Development Group (2017) Capacity Development, UNDAF companion guidance. https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance 

The indicator for this target monitors the amount of `Official development assistance` as part of government WASH spending plans, `ODA` is included as a capacity building term as well as `grants` and `loans` https://unstats.un.org/sdgs/metadata/files/Metadata-06-0A-01.pdf (UNstats2025)

`ABOUT CAPACITY BUILDING IN OLD VERSION ON 13.3` https://github.com/SDGforskning/sdg-strings/blob/v1.0.0/SDG13_query_action_WoS.md#target-133
`TEST/READ ABOUT TECHNOLOGY TRANSFER AS PART OF CAPACITY BUILDING SUPPORT`

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (United Nations, 2016, 2017, 2018, 2019, 2020, 2021). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).


#### Phrase 1

The elements of the phrase are *action + capacity building/international cooperation + WASH/drinking water/water harvesting/desalination/water efficiency/wastewater treatment/recycling and reuse of water + developing countries*

The structure of the phrase is similar to SDG 12.a phrase 1.



```py
TS=
(
(
    ("develop" OR "development" OR "promote" OR "strengthen*" OR "improv*" OR "enhanc*" OR "increas*" OR "build" OR "building" OR "advance" OR "advancing" 
    OR "establish*" OR "address" OR "consider*" OR "assess*" OR "expand*" OR "support*"
    )
    NEAR/5
    (
      ("institutional capacity" OR "human capacity" OR "technological capacity" OR "scientific capacity" OR "financial capacity" 
      OR "capacity building" OR "capacity development" OR "build* capacity" OR "develop* capacity" 
      OR "infrastructure$" OR "facilities" OR "tools" OR "technical support" OR "managerial support"
      OR "research" OR "knowledge" OR "skills" OR "competenc*" OR "expertise" OR "R&D" OR "innovation" 
      OR "communication" OR "social network$" OR "information network$" OR "campaign$" 
      OR "awareness" OR "disseminat*" OR "educat*" OR "training" 
      OR "knowledge transfer*" OR "transfer of technolog*" OR "technological transfer" OR "technology transfer"
      OR "expenditure" OR "invest" OR "investing" OR "investment$" OR "financing" OR "spending" OR "funding" OR "funder$" OR "fund$" OR "grant$" OR "loan$"
      OR "financial support" OR "financial resources"
      OR "incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
      OR "ODA" OR "official development assistance" OR "cooperation fund$" OR "development spending" OR "development aid" OR "development assistance" OR "foreign aid" OR "international aid" OR "international assistance"
      OR "policy" OR "policies" OR "empower*" OR "strateg*" OR "programme$" OR "program$" OR "intervention$" 
      OR "international cooperation" OR "international collaboration" 
      OR "international network$" OR "international partnership$"
      OR "development cooperation" OR "development network$"
      OR "development partnership$" OR "research partnership$"
      OR (("international" OR "development") 
        NEAR/3 ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"))
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
)
AND 
    ("least developed countr*" OR "least developed nation$"
    OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
    OR "less developed countr*" OR "less developed nation$" OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$" OR "underserved countr*" OR "underserved nation$" OR "deprived countr*" OR "deprived nation$"
    OR "middle income countr*" OR "middle income nation$"
    OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
    OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
    OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
    OR  "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"      OR  "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"      OR  "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"      OR   "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish"  OR "turkey" OR "georgia"
    )
)
```

### Target 6.b

> **6.b Support and strengthen the participation of local communities in improving water and sanitation management**
>
> 6.b.1 Proportion of local administrative units with established and operational policies and procedures for participation of local communities in water and sanitation management

This target is interpreted to cover research about supporting the participation of local communities and stakeholders in water and sanitation management. As the indicator for this target https://unstats.un.org/sdgs/metadata/files/Metadata-06-0B-01.pdf (“UNstats2025”) measures existing `administrative units` `policies` and `procedures` for local community participation, we include these in participation. Even though the focus of the target is on local participation rather than administration https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf   
(“DESA2018”)

According to the indicator metadata 6.b, water and sanitation management includes all areas of management related to each of the targets under SDG 6:  water supply (6.1), sanitation and hygiene (6.2), wastewater treatment and ambient water 
quality (6.3), efficiency and sustainable use (6.4), integrated water resources management (6.5) and water-related ecosystems (6.6).

#### Phrase 1

The elements of the phrase are *action + local communities + participation/policies + WASH + management*


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

UN Statistics Division (2025). *SDG Indicators Metadata Repository*. https://unstats.un.org/sdgs/metadata ("UNstats2025")

UN Department of Global Communications (2023). What Is Goal 6 –Clean Water And Sanitation https://www.un.org/sustainabledevelopment/wp-content/uploads/2023/09/Goal-6_Fast-Facts.pdf ("UNDeptofComm2023") 

UN DESA (2023). HLPF Factsheet SDG 6 https://sdgs.un.org/sites/default/files/2023-07/2023%20HLPF%20Factsheet%20SDG%206.pdf ("DESAfact2023")

UN DESA/DSDG et al. (2018). 2018 HLPF Review of SDG implementation: SDG 6 – Ensure availability and sustainable management of water and sanitation for all https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf   ("DESA2018")

High-level Political Forum (2023). SDGs in focus: SDG 6 and interlinkages with other SDGs – Clean water and sanitation https://hlpf.un.org/sites/default/files/2023-06/BN%20HLPF%202023%20SDG%206_1.pdf ("HLPF2023")

HLPF (2018). Inclusive, Safe, Resilient and Sustainable Societies and Persons with Disabilities: Executive Summary
https://sdgs.un.org/sites/default/files/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf ("HLPF2018")

UNSD (2022). 6 Clean Water and Sanitation: The Sustainable Development Goals Extended report 2022 https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf ("UNSDextended2022")

UN-Water. WASH - Water, Sanitation and Hygiene https://www.unwater.org/water-facts/wash-water-sanitation-and-hygiene ("WASH") [Accessed 2025.04.28]

UN-Water. Water and Gender https://www.unwater.org/water-facts/water-and-gender (“Water&Gender”) [Accessed 2025.04.28]

UN-Water. Water Quality and Wastewater https://www.unwater.org/water-facts/water-quality-and-wastewater ("WASTE") [Accessed 2025.04.29]

UN-Water. Water and Ecosystems https://www.unwater.org/water-facts/water-and-ecosystems ("ECO") [Accessed 2025.04.29]

WHO (2023). Drinking-water https://www.who.int/news-room/fact-sheets/detail/drinking-water (WHO2023)

United Nations (n.d.) Fight racism. Vulnerable groups, who are they?. https://www.un.org/en/fight-racism/vulnerable-groups?gclid=EAIaIQobChMI9ODI_PvC9wIVV53VCh3pQgZCEAAYASAAEgInB_D_BwE (accessed Jun 2022).("UNracism")

Office of the High Commissioner (n.d.) Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health. United Nations Human Rights. https://www.ohchr.org/en/special-procedures/sr-health/non-discrimination-groups-vulnerable-situations (accessed Jun 2022). ("NonDiscr")

Blanchard et al. (2017). Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment. United Nations Office for Disaster Risk Reduction. https://www.undrr.org/publication/marginalized-and-minority-groups-consideration-ndra. ("Blanchard")

United Nations Development Group (2017) Capacity Development, UNDAF companion guidance. https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance [accessed 19.12.2019] 
