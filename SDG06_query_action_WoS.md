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

The elements of the phrase are *action + unsafe/unprotected/contaminated + drinking water sources*

```py
TS=
(

)
```


### Target 6.2

> **6.2 By 2030, achieve access to adequate and equitable sanitation and hygiene for all and end open defecation, paying special attention to the needs of women and girls and those in vulnerable situations**
>
> 6.2.1 Proportion of population using (a) safely managed sanitation services and (b) a hand-washing facility with soap and water

This target is interpreted to cover research about 

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

UN Statistics Division (2025). *SDG Indicators Metadata Repository*. https://unstats.un.org/sdgs/metadata ("UNstats2025")

UN Department of Global Communications (2023). What Is Goal 6 –Clean Water And Sanitation https://www.un.org/sustainabledevelopment/wp-content/uploads/2023/09/Goal-6_Fast-Facts.pdf ("UNDeptofComm2023") 

UN DESA (2023). HLPF Factsheet SDG 6 https://sdgs.un.org/sites/default/files/2023-07/2023%20HLPF%20Factsheet%20SDG%206.pdf ("DESAfact2023")

UN DESA/DSDG et al. (2018). 2018 HLPF Review of SDG implementation: SDG 6 – Ensure availability and sustainable management of water and sanitation for all https://hlpf.un.org/sites/default/files/migrated/documents/195716.29_Formatted_2018_background_notes_SDG_6.pdf   ("DESA2018")

High-level Political Forum (2023). SDGs in focus: SDG 6 and interlinkages with other SDGs – Clean water and sanitation https://hlpf.un.org/sites/default/files/2023-06/BN%20HLPF%202023%20SDG%206_1.pdf ("HLPF2023")

HLPF (2018). Inclusive, Safe, Resilient and Sustainable Societies and Persons with Disabilities: Executive Summary
https://sdgs.un.org/sites/default/files/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf ("HLPF2018")

UNSD (2022). 6 Clean Water and Sanitation: The Sustainable Development Goals Extended report 2022 https://unstats.un.org/sdgs/report/2022/extended-report/Extended-Report_Goal-6.pdf ("UNSDextended2022")

UN Water. WASH - Water, Sanitation and Hygiene https://www.unwater.org/water-facts/wash-water-sanitation-and-hygiene ("WASH") [Accessed 2025.04.28]
