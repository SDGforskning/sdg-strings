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

This target is interpreted to cover research about advancing access to safe and affordable drinking water for all people. It also includes steps necessary for achieving this, for example `safe management of drinking water services` which is an indicator of this target and `investments in infrastructure`. Some steps towards safe drinking water are covered in detail by other targets of SDG 6 and are not included here. 

Together, targets 6.1 and 6.2 form the WASH targets. *The health and socio-economic benefits of safely managed water can only be fully realized alongside safely managed sanitation and good hygiene practices.*  https://www.unwater.org/water-facts/wash-water-sanitation-and-hygiene ("WASH") Some gender specific features about access to safe drinking water (fetching water) are covered in the phrases for target 6.2 which aims to find research about gender inequalities related to WASH.

Target 6.1 is related to SDG 11 target 11.1 which is about access to safe housing and basic services.




```
????

Collection/fetching water is important from gender inequalities point of view.
It is mostly done by women & girls and is time consuming which precludes them from school or work
and also makes them vulnerable to attack https://www.unwater.org/water-facts/water-and-gender.

As it is especially related to women and 6.2 covers paying attention to women etc. should we move it there?
Although 6.2 is about sanitation & hygiene, not drinking water.
Still, WASH is ofen discussed as a unite and some sources (Wikipedia) even mention clean drinking water as an element of sanitation.

Even in 6.2 it is difficult to include in an action phrase *prevent/decrease + women fetching water* sounds harsh/strange.
Should we use it only in topic phrases? 

```




#### Phrase 1

This phrase aims to find research about advancing accessibility to safe and affordable drinking water and about promoting and investing in safely managed drinking water services and infrastructures. By the definition of the indicator metadata 6.1.1 safely managed drinking water services refer to using `improved drinking water sources` which are accessible, available when needed and free from contamination. The indicator metadata definitions for accessability and availability would have been difficult to incorporate in the phrase, we have just search for any research mentioning accessable or available drinking water.

Terms for improved drinking water sources were found from the indicator 6.1.1 metadata https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf.  (“UNstats2025”).

The elements of the phrase are *action(advance/invest/) + access/availability/affordability/management/regulating + safe + drinking water + services/sources/infrastructures*

```py
TS=
(

)
```

#### Phrase 2

This phrase aims to find research about reducing the use of unsafe drinking water, i.e. drinking water from unimproved water sources or contaminated drinking water. Definitions for unimproved water sources and biological or chemical contaminants of drinking water were found from the indicator metadata 6.1.1. https://unstats.un.org/sdgs/metadata/files/Metadata-06-01-01.pdf (“UNstats2025”)

The elements of the phrase are *action + unsafe/unprotected/contaminated + drinking water/sources*

```py
TS=
(

)
```


### Target 6.2

> **6.2 By 2030, achieve access to adequate and equitable sanitation and hygiene for all and end open defecation, paying special attention to the needs of women and girls and those in vulnerable situations**
>
> 6.2.1 Proportion of population using (a) safely managed sanitation services and (b) a hand-washing facility with soap and water

This target is interpreted to cover research about advancing adequate and equitable access to sanitation and hygiene for all people and in particular women and girls and people in vulnerable situations. It is also about abandoning unimproved sanitation facilities or lack of sanitation i.e. practicing open defecation. https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf (”DESA2018”).

What is adequate sanitation? According to the definitions of the indicator metadata 6.2.1a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (“UNstats2025”) 

> *Safely managed sanitation services is about using improved sanitation facilities*.
> 
> *Use of improved sanitation facilities which are not shared is defined as a basic sanitation service.
> While the use of shared improved  sanitation facilities is defined as limited sanitation service*.
> 
> *Safely managed sanitation services also refer to facilities where the excreta are safely disposed of in situ or removed
> and treated off-site and hygienically separate from human contact*.

However, we have built the search phrases to search for any research mentioning advancing access to adequate/safe sanitation i.e. the phrases search for adequate as it has been defined in the found research. 




```
????

Maybe we should stick to the metadata definition about adequate.
But the definition is complex and with a quick test, nothing is found with the defined terms & combinations.

```




As the target is about equal access and a particular focus is on women, girls and people in vulnerable situations we interpret this target also to include eliminating inequalities they may face in access to sanitation and hygiene. We have also included gender dependent inequalities related to the acquisition of drinking water. Even though drinking water is not unambiguously defined as part of sanitation there is a strong interlinkage between water, sanitation and hygiene https://www.unwater.org/water-facts/wash-water-sanitation-and-hygiene ("WASH").

#### Phrase 1

This phrase aims to find research about providing access to adequate and safe sanitation and hygiene for all people. Terms for the search were found e.g. in the indicator metadata 6.2.1a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (UNstats2025).

The elements of the phrase are *action + access + adequate/safe/basic/improved + service/facility + sanitation/hygiene* 


```py
TS=
(

)
```

#### Phrase 2

This phrase aims to find research about abandoning lack of sanitation or unsafe i.e. unimproved sanitation such as practicing open defecation as well as lack of hygiene services.

Terms for unimproved sanitation were found from indicator metadata 6.2.1 a https://unstats.un.org/sdgs/metadata/files/Metadata-06-02-01a.pdf (“UNstats2025”)

The elements of the phrase are *action + inadequate/unsafe/unimproved/lacking + service/facility + sanitation/hygiene*


```py
TS=
(

)
```

#### Phrase 3

This phrase aims to find research about eliminating inequalities in access to safe sanitation and hygiene services particularly for women, girls and people in vulnerable situations. 

HLPF review on SDG 6 implementation (2018) https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf ("DESA2018") states that universal access also implies providing access to services in schools, health-care facilities and other institutional settings. We have not added these as specific terms in the phrases since they are covered by the general syntax 
`access` + `sanitation/hygiene services` + `women/girls/people in vulnerable situations`.

Terms for removing barriers or facilitating access to sanitation/hygiene services for persons with disabilities were found in https://sdgs.un.org/sites/default/files/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf
("HLPF2018").

Terms for marginalized communities are from  https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf ("DESA2018")

We used UN sources to find terms and groups that can be considered "vulnerable" (Blanchard et al., 2017; Office of the High Commissioner, n.d.; United Nations, n.d.).

* United Nations (n.d.) Fight racism. Vulnerable groups, who are they?. https://www.un.org/en/fight-racism/vulnerable-groups?gclid=EAIaIQobChMI9ODI_PvC9wIVV53VCh3pQgZCEAAYASAAEgInB_D_BwE (accessed Jun 2022).("UNracism")

* Office of the High Commissioner (n.d.) Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health. United Nations Human Rights. https://www.ohchr.org/en/special-procedures/sr-health/non-discrimination-groups-vulnerable-situations (accessed Jun 2022). ("NonDiscr")

* Blanchard et al. (2017). Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment. United Nations Office for Disaster Risk Reduction. https://www.undrr.org/publication/marginalized-and-minority-groups-consideration-ndra. ("Blanchard")

The elements of the phrase are *action(eliminate inequalities/remove barriers/non-discriminating OR facilitate/assist/support) + access + services/facilities + sanitation/hygiene + women/girls/vulnerable people* 


```py


SKETCH
TS=
(
(
  (
  ((eliminate OR remove) 
AND 
      (
      (inequalities OR discrimination OR barriers) 
      OR 
      (narrow entrances OR steps OR lack of space)
      ) 
  )
  OR
  (facilitate OR assist OR support)
  )

    AND 
    (
    (access)
    AND 
		  (
		  (services OR facilities) 
		  AND (sanitation OR hygiene)
		  ) 
    )
)
AND ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "living in poverty"
    OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
    OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" 
    OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
    OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
    OR (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
    OR "disabled" OR "disabilities" OR "disability"
    OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
    OR "unemployed" 
    OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*" OR "accident$"))
    OR "women" OR "woman" OR "girls" OR "girl"
    OR "pregnant" OR "pregnancy" OR "maternity"
    OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
    OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
    OR "living with HIV" OR "living with AIDS"
    OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
    OR "indigenous group$"
    )
)

```

#### Phrase 4

This phrase aims to find research about removing gender related inequalities concerning the burden of fetching water from remote water sources. Collection/fetching water is usually done by women and girls and as it is time consuming it often precludes them from school or making incomes at work. It can also make them vulnerable to attack https://www.unwater.org/water-facts/water-and-gender (“Water&Gender”)

The elements of the phrase are *remove inequalities + collecting/fetching water + women/girls*

```
????

Should phrase 4 be here? Difficult to place in 6.1 but should be somewhere.


```



```py
TS=
(

)
```



### Target 6.3

> **6.3 By 2030, improve water quality by reducing pollution, eliminating dumping and minimizing release of hazardous chemicals and materials, halving the proportion of untreated wastewater and substantially increasing recycling and safe reuse globally**
>
> 6.3.1 Proportion of domestic and industrial wastewater flows safely treated
>
> 6.3.2 Proportion of bodies of water with good ambient water quality

This target is interpreted to cover research about improving water quality by reducing the proportion of untreated wastewaters discharged into the environment as well as releases of pollution and hazardous chemicals and materials. It is also about increasing recycling and safe reuse of water and monitoring of water quality https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf (“UNSDextended2022”); https://www.unwater.org/water-facts/water-quality-and-wastewater ("WASTE")

This target focuses on freshwater bodies, the ones mentioned in the 6.3.2 indicator metadata are `lakes` `rivers` `streams` `groundwaters` `aquifers`  `reservoirs` . The classification for wastewater generators is 
> * domestic/households
> * industrial
> * services
> https://unstats.un.org/sdgs/metadata/files/Metadata-06-03-02.pdf (“UNstats2025)
> 
> Runoff from urban and agricultural land is counted as wastewater but not monitored systematically
> https://unstats.un.org/sdgs/metadata/files/Metadata-06-03-01.pdf (“UNstats2025)

Target 6.3 is related to targets 
* SDG 14.1 preventing and reducing marine pollution
* SDG 12.4 reducing harmful releases to water
* SDG 12.5 reducing waste through e.g. recycling and reuse

#### Phrase 1

This phrase aims to find research about reducing or eliminating releases of pollution and hazardous chemicals and dumping into fresh water bodies as well as reducing untreated wastewaters.

The elements of the phrase are *action + untreated wastewaters/wastewater generation/releases/pollution/hazardous chemicals/dumping + fresh water bodies*


```py
TS=
(

)
```

#### Phrase 2

This phrase aims to find research about increasing or improving water quality, treatment of wastewaters, recycling and safe reuse of water.

The elements of the phrase are *action(increase/improve/manage) + treatment of wastewaters/water quality/monitoring/recycling/safe reuse + water*


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

Definitions of **Water stress**, **Total freshwater withdrawal (TFWW)** and **Total renewable freshwater resources (TRWR**) as defined by the indicator metadata 6.4.2 https://unstats.un.org/sdgs/metadata/files/Metadata-06-04-02.pdf (“UNstats2025”)

> **Total freshwater withdrawal (TFWW)** is *the volume for freshwater extracted from its source (rivers, lakes, aquifers) for agriculture,
>  industries and services. Withdrawal includes fossil groundwater. It does not include non-conventional water, i.e. `treated wastewater`,
>  `agricultural drainage water` or `desalinated water`*
>
> **Total renewable freshwater resources (TRWR)** are *the sum of internal and external freshwater resources*.
>
> **The level of water stress** is *the ratio between total freshwater withdrawal and total revewable freshwater resources*.

#### Phrase 1

This phrase aims to find research about increasing water-use efficiency, sustainable withdrawals and water savings on all sectors.

Terms were found in 
* UNSD SDG 6 extended report 2022 (“UNSDextended2022”)
* Indicator metadata 6.4.1 https://unstats.un.org/sdgs/metadata/files/Metadata-06-04-01.pdf (“UNstats2025”)
* terms for increasing water savings in agriculture https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf   
(“DESA2018”)

The elements of the phrase are *action + WUE/sustainable withdrawals/water savings + sectors*

#### Phrase 2

This phrase aims to find research about reducing water stress, water scarcity and unsustainable water withdrawals on all sectors.

The elements of the phrase are *action + unsustainable withdrawals+sectors/water stress/water scarcity*



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

This target is interpreted to cover research about implementing integrated water resources management and transboundary co-operation in water resources management. 

**Integrated water resources management (IWRM)** is based on an internationally agreed definition.
> *Integrated Water Resources Management (IWRM) promotes the coordinated development and management of water, land and related resources to
>  maximize economic and social welfare in an equitable manner, without compromising the sustainability of vital ecosystems*.

Indicator metadata 6.5.1 https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-01.pdf ("UNstats2025")

IWRM is a cross-sectoral approach to water resources management based on the interdependence of uses of water resources on different sectors. It consists of various dimensions including enabling environment (policies, laws, etc), roles of supporting institutions, management instruments for choices between alternative actions and financing.

Since IWRM is a specifically defined consept the phrase is set to look for research which explicitly mentions IWRM rather than looking for any cross-sectoral water research management.

Transboundary co-operation refers to operational agreements on water management between countries sharing transboundary rivers, lakes and aquifers. 


```
????


Should we search only for defined IWRM or should we search for any cross-sectoral water management?


```

#### Phrase 1

This phrase aims to find research about implementing IWRM or transboundary co-operation.

Terms were found from 
* Indicator metadata 6.5.1  https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-01.pdf ("UNstats2025")
* Indicator metadata 6.5.2 https://unstats.un.org/sdgs/metadata/files/Metadata-06-05-02.pdf.
* Terms for water management related projects and programmes were found in https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf ("UNSDextended2022")

The elements of the phrase are *action(implement/advance) + IWRM OR
arrangement/treaty/agreement+co-operation/collaboration +  crossboundary/international+water basin+management/projects*


```py



SKETCH
TS=
(
("implement*" OR "advanc*" OR "promot*") 
AND 
	("integrated water resources management" OR ("IWRM" NEAR "water"))
	OR
	(
		(
		("arrangement*" OR "treaty" OR "treaties" OR "agreement*" OR "framework*")
		NEAR/5
			("co-operation" OR "cooperation" OR "collaboration")
		)
		AND
		(
		(
		("crossboundary" OR "crossborder")
		NEAR/5
			("water basin*" OR "lake*" OR "river*" OR "stream*" OR "aquifer*" OR "groundwater*")
		)
		NEAR/15
		("management" OR "hydroelectric*" OR "agriculture" OR ("protected area*" NEAR "conservation"))
		
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

```


?????


No action term in the summary of the target (e.g. increase+protection – just protect)
> Action and Topic phrases will be identical.

Should we include protection of species/biodiversity? They are mentioned in sources but the focus is clearly in protecting water.
We could add them in phrase 2 deterioration terms (loss of biodiversity / extinction of species)?

Conflict: mountains and forests are mentioned in the title of the target
but in indicator metadata 6.6.1 they are listed as excluded because they are covered by SDG 15.
No reason to add "forest" or "mountains" to phrases - water-related ecosystems within them will be found anyway.
I suppose no nead to filter them out even though the indicator excludes them?


```

#### Phrase 1 
(see 15.1 phrase 2)

This phrase aims to find research about protecting freshwater-related ecosystems, their spatial extent and water quality and quantity.

The elements of the phrase are *protect + ecosystems/areas/water quality/water quantity + water-related ecosystems*


```py
TS=
(

)
```

#### Phrase 2

This phrase aims to find research about halting the deterioration of water-related ecosystems.

Terms for deterioration were found in UNSD SDG 6 Extended report 2022 https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf (“UNSDextended2022”)

The elements of the phrase are *action(stop) + decline/deterioration/unsustainable use/loss/poor quality + water-related ecosystems*


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
