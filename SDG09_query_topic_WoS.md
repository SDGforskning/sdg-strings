# Search query for SDG 9 - Industry, innovation and infrastructure, Bergen topic-approach.

Build resilient infrastructure, promote inclusive and sustainable industrialization and foster innovation 

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the topics in the SDG 9 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in the SDG 9 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).


## 3. Targets

### Target 9.1

> **9.1 Develop quality, reliable, sustainable and resilient infrastructure, including regional and transborder infrastructure, to support economic development and human well-being, with a focus on affordable and equitable access for all**
>
> 9.1.1 Proportion of the rural population who live within 2 km of an all-season road
>
> 9.1.2 Passenger and freight volumes, by mode of transport

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 9.2

> **9.2 Promote inclusive and sustainable industrialization and, by 2030, significantly raise industry’s share of employment and gross domestic product, in line with national circumstances, and double its share in least developed countries**
>
> 9.2.1 Manufacturing value added as a proportion of GDP and per capita
>
> 9.2.2 Manufacturing employment as a proportion of total employment

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 9.3

> **9.3 Increase the access of small-scale industrial and other enterprises, in particular in developing countries, to financial services, including affordable credit, and their integration into value chains and markets**
>
> 9.3.1 Proportion of small-scale industries in total industry value added
>
> 9.3.2 Proportion of small-scale industries with a loan or line of credit

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 9.4

> **9.4 By 2030, upgrade infrastructure and retrofit industries to make them sustainable, with increased resource-use efficiency and greater adoption of clean and environmentally sound technologies and industrial processes, with all countries taking action in accordance with their respective capabilities**
>
> 9.4.1 CO2 emission per unit of value added

This target is interpreted to cover research about sustainable infrastructure and industry achieved through resource-use efficiency and the adoption of clean and environmentally sound technologies and industrial processes.

See Target 9.1 for details on how we define the concept of infrastructure.

This query consists of one phrase.

#### Phrase 1

This phrase is about the sustainability of infrastructure and industry through resource efficiency and the usage of clean and environmentally friendly technologies and industrial processes. Basic structure is *sustainability + infrastructure/industry + resource-use efficiency /clean technologies / environmentally sound*.

```py
TS=
(
    ("sustainab*" OR "resilien*" OR "adaptab*" OR "flexib*" OR "maintainable*" OR "renewabl*" OR "resource-efficien*" OR "repairab*" 
	OR "recyclab*" OR "reusab*" OR "ecofriendly" OR "eco-friendly" OR "environmentally friendly" OR "environmentally sound" OR "ecologically friendly" OR "ecologically sound" OR "low* carbon" OR "green" OR "eco" OR "ecological" OR "nonpolluting" OR "energy-efficient"
    ) 
	    NEAR/5 
        (
            ("infrastruct*" OR "industry" OR "industries" OR "manufacturer$" OR "industrial sector$"
            OR "infrastruct*" OR (("energy" OR "power") NEAR/1 ("infrastruct*" OR "supply" OR "solution$" OR "source*")) 
            OR "energy system$" OR "power system$" 
            OR "electrification" OR "electric* transmission" OR "electric* distribution" OR "electric* connections" OR "electric* production" OR "lighting" 
            OR (("waste" OR "wastewater$" OR "sewage") NEAR/1 ("treatment" OR "collection" OR "management")) OR "recycling system$" 
            OR "water supply" OR "drinking water" OR "clean water" OR "sanitation" OR "drainage system$" OR "water and sanitation system$" OR "food supply"
            OR "telecommunication$" OR "digital communications" OR "communication$" OR "digital solutions" OR "internet" OR "mobile network$"
            OR "public amenities" OR "rule of law" OR "juridical system$" OR "legal services" OR "financial service$" OR "banking service$" OR "education" OR "school$" 
            OR "health care" OR "healthcare" 
            OR "buildings" OR "housing" OR "public spaces" OR "disaster management" 
            OR "mass transit*" OR "mobility system$" OR "public transport*" OR "public transit*" OR "transport" OR "transportation" OR "urban mobility" OR "road" OR "roads"
            )  
	        NEAR/5
            (
                (("resourse$" OR "water" OR "material$" OR "energy") NEAR/1 ("efficien*" OR "sustainable" OR "optimi$ation")) 
                OR "eco-efficien*" OR "circular econom*" OR "circularity" OR "closed-loop economy" 
                OR "industrial ecology" OR "cradle to cradle" OR "cradle-to-cradle"
                OR (("sustainab*" OR "environmental*" OR "ecological*" OR "eco" OR "green" OR "clean" OR "cleaner") NEAR/1 ("technolog*" OR "practice$" OR "production" OR "process*")) 
                OR (("footprint" OR (("lifecycle$" OR "life-cycle$") NEAR/1 "cost$")) NEAR/3 ("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "lower" OR "lower$" OR "lowered"))
		    )
        )

)
```

### Target 9.5

> **9.5 Enhance scientific research, upgrade the technological capabilities of industrial sectors in all countries, in particular developing countries, including, by 2030, encouraging innovation and substantially increasing the number of research and development workers per 1 million people and public and private research and development spending**
>
> 9.5.1 Research and development expenditure as a proportion of GDP
>
> 9.5.2 Researchers (in full-time equivalent) per million inhabitants

SDG Target 9.5 focuses on strengthening the foundation for innovation and scientific advancement. E-Handbook on Sustainable Development Goals Indicators (2024): 9.5.1 and 9.5.2. In spite of the research workforce continuing to rise at the global level, firm policy commitments towards substantial increase in the number of research personnel, particularly in developing economies, as well as strengthening the participation of women in research profession are essential for the effective delivery of innovative solutions for the challenges ahead. The Sustainable Development Goals. Extended Report 2024. (2024)  

This target is interpreted to cover research about:    

    Increasing technological capabilities and research within or to do with industry  

    Increasing innovation, and increasing R&D capacity, including workforce and funding  

This query consists of one phrase. The elements of the phrase are research/innovation/R&D/technology + industry/capability/workforce.

```py
TS=
(
     ("research" OR "innovation*" OR "R&D" OR "R & D" OR "research and development" OR "research & development" OR "technology" OR "technological capabilities" 
     )  
        NEAR/5 
        ("industr*" OR "capacity" OR "capabilit*" OR "sector*" OR "institutions" OR "national" OR "regional" OR "worker*" OR "workforce" OR "researcher$" OR "invest*" OR "financ*" OR "fund*" OR "spending*" OR "expend*" OR "expense*" OR "GDP" OR "subsidy" OR "subsidi*" ) 
) 
```

### Target 9.a

> **9.a Facilitate sustainable and resilient infrastructure development in developing countries through enhanced financial, technological and technical support to African countries, least developed countries, landlocked developing countries and small island developing States**
>
> 9.a.1 Total official international support (official development assistance plus other official flows) to infrastructure

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 9.b

> **9.b Support domestic technology development, research and innovation in developing countries, including by ensuring a conducive policy environment for, inter alia, industrial diversification and value addition to commodities**
>
> 9.b.1 Proportion of medium and high-tech industry value added in total value added

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 9.c

> **9.c Significantly increase access to information and communications technology and strive to provide universal and affordable access to the Internet in least developed countries by 2020**
>
> 9.c.1 Proportion of population covered by a mobile network, by technology
> 
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

<span id="f1">UN DESA. (2025).</span> *Goals: Build resilient infrastructure, promote inclusive and sustainable industrialization and foster innovation *. https://sdgs.un.org/goals/goal9#targets_and_indicators [Accessed 2025.04.02]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/
