# Search query for SDG 8 - Decent work and economic growth, Bergen action-approach.

Promote sustained, inclusive and sustainable economic growth, full and productive employment and decent work for all

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 8 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 8 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Health (https://epoc.cochrane.org/lmic-filters).

## 3. Targets

### Target 8.1

> **8.1 Sustain per capita economic growth in accordance with national circumstances and, in particular, at least 7 per cent gross domestic product growth per annum in the least developed countries**
>
> 8.1.1 Annual growth rate of real GDP per capita

This target is interpreted to cover research about 

* sustaining per capita economic growth
* supporting national macroeconomic development

This includes work focused on productivity, GDP growth, and development models in both individual per capita and national terms. While the goal highlights Least Developed Countries (LDCs), relevant literature may also examine comparative or general economic strategies, particularly where equity and sustainability are addressed.

```py
TS=
(

)
```

### Target 8.2

> **8.2 Achieve higher levels of economic productivity through diversification, technological upgrading and innovation, including through a focus on high-value added and labour-intensive sectors**
>
> 8.2.1 Annual growth rate of real GDP per employed person

This target is interpreted to cover research about 
* Increasing economic productivity through diversification, technological upgrading and innovation.

The focus is on economic productivity in general, and the two latter aspects, high-value added and labour-intensive sectors, are treated as examples and included in the search strings but not in the interpretation.

```py
TS=
(

)
```

### Target 8.3

> **8.3 Promote development-oriented policies that support productive activities, decent job creation, entrepreneurship, creativity and innovation, and encourage the formalization and growth of micro-, small- and medium-sized enterprises, including through access to financial services**
>
> 8.3.1 Proportion of informal employment in total employment, by sector and sex

This target is interpreted to cover research about
* Promoting policies that support productive activities, decent job creation, entrepreneurship, creativity and innovation
* Promoting policies that encourage formalization and growth micro-, small- and medium-sized enterprises

The aspect of development-oriented policies is dificult to distinguish and not emphasized in the interpretation. There is some overlap with other SDGs (decent job creation, innovation and growth).

```py
TS=
(

)
```

### Target 8.4

> **8.4 Improve progressively, through 2030, global resource efficiency in consumption and production and endeavour to decouple economic growth from environmental degradation, in accordance with the 10-Year Framework of Programmes on Sustainable Consumption and Production, with developed countries taking the lead**
>
> 8.4.1 Material footprint, material footprint per capita, and material footprint per GDP
>
> 8.4.2 Domestic material consumption, domestic material consumption per capita, and domestic material consumption per GDP

This target is interpreted to cover research about
* Improving resource efficiency in consumption and production
* Endeavouring to decouple economic growth from negative environmental impact

The focus is on resource efficiency, and not limited to the global aspect and progressive improvement. The framing of the target is the Framework of Programmes on Sustainable Consumption and Production (10YFP) with base documents and interim progress reports.

```py
TS=
(

)
```

### Target 8.5

> **8.5 By 2030, achieve full and productive employment and decent work for all women and men, including for young people and persons with disabilities, and equal pay for work of equal value**
>
> 8.5.1 Average hourly earnings of female and male employees, by occupation, age and persons with disabilities
>
> 8.5.2 Unemployment rate, by sex, age and persons with disabilities

This target is interpreted to cover research about 

* achieving full employment
* creating employment and jobs, labour rights, ensuring social protection for workers, ensuring social dialogue in workplaces, and more generally having access to decent work and employment
* improving wage equality

This includes studies on both the quantity and quality of employment, including issues like underemployment, labor market discrimination, job satisfaction, working conditions, and wage fairness. While women, youth, and persons with diabilities are mentioned specifically, searches should capture broader issues of inclusion and equity across labor markets.

Decent work is defined by ILO in their Decent Work Agenda and contains the four pillars of 'employment creation, social protection, rights at work, and social dialogue' <a href="#f3">(ILO, 2025)</a>. Productive employment is defined by ILO as 'employment yielding sufficient returns to labour to permit the worker and her/his dependents a level of consumption above the poverty line' <a href="#f4">(ILO, 2017)</a>

```py
TS=
(

)
```

### Target 8.6

> **8.6 By 2020, substantially reduce the proportion of youth not in employment, education or training**
>
> 8.6.1 Proportion of youth (aged 15-24 years) not in education, employment or training

This target is interpreted to cover research about reducing the number of youth not in employment, education, or training (NEET).

This includes research on youth disengagement, early labor market integration, and various interventions (educational, policy-based, or community-driven) aimed at increasing youth participations in economic and educational systems.

This query consists of two phrases. Phrase 1 addresses the issue of reducing unemployment in youth, whereas Phrase 2 is concerned with increasing employment of the same group of people.

#### Phrase 1

The basic structure is *action + drop-out + youth + education/training* and *action + unemployment + youth*

```py
TS=
(
  (
    ("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" 
	OR "combat*" OR "declin*" OR "abate$" OR "abating" OR "diminish*")
    NEAR/10
    (
      (
        ("dropout*" OR "drop-out*" OR "drop out" OR "dropping out" OR "quit" OR "early school-leaving" OR "withdraw$" OR "withdrawal$" OR "discontinue")
        NEAR/10
        ("youth*" OR "young people" OR "adolescen*" OR "teen*" OR "young adult*")
        NEAR/15
        (
          "education" OR "schooling" OR "academic*" OR "academia" OR "apprenticeship$" OR "internship" OR "reskill$" OR "reskilling" OR "professional development" OR "primary school*" OR "elementary school*" 
		  OR "primary educat*" OR "middle school*" OR "secondary school*" OR "secondary education*" OR
          (
            ("school" OR "education") NEAR/3 ("boys" OR "girls" OR "kids" OR "child*")
          ) OR
          "university" OR "universities" OR "higher education" OR "college$" OR
          (
            ("technic*" OR "vocation*" OR "tertiar*" OR "postsecondary" OR "post secondary")
            NEAR/3
            ("education" OR "training" OR "school*" OR "learning")
          ) OR
		  (
		  ("skill$" OR "job" OR "career" OR "workforce") NEAR/3 "training"
		  )
        )
      )
      OR
      (
        ("unemploy*" OR "underemploy*" OR "NEET$" OR "jobless" OR "out of work" OR "not in work" OR "economic* inactive" OR "labor market exclusion$" OR "labour market exclusion$" OR "employment barrier$")
        NEAR/10
        ("youth*" OR "young people" OR "adolescen*" OR "teen*" OR "young adult*")
      )
    )
  )
)
```

#### Phrase 2

In this phrase we shift the emphasis from decreasing the number of youth not in employment, education, or training (NEET) to actively increasing the proportion of youth who are engaged in employment, education, or training.

The basic structure is *action + completion + youth + education/training* and *action + employment + youth*

```py
TS=
(
  (
    ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "upgrad*" OR "build$" OR "building" OR "expand" OR "expansion*" OR "encourag*" OR "facilitat*" OR "promot*" 
	OR "raise" OR "raising" OR "raised" OR "foster*" OR "boost*" OR "ensure" OR "attain*" OR "achiev*")
    NEAR/10
    (
      (
        ("completion" OR "attainment" OR "graduation" OR "academic success" OR "access" OR "skill$ acquisition" OR "retention")
        NEAR/5
        ("youth*" OR "young people" OR "adolescen*" OR "teen*" OR "young adult*")
        NEAR/5
        (
          "education" OR "schooling" OR "academic*" OR "academia" OR "apprenticeship$" OR "internship" OR "reskill$" OR "reskilling" OR "professional development" OR "primary school*" OR "elementary school*" 
		  OR "primary educat*" OR "middle school*" OR "secondary school*" OR "secondary education*" OR "school-to-work transition$" OR
          (
            ("school" OR "education") NEAR/3 ("boys" OR "girls" OR "kids" OR "child*")
          ) OR
          "university" OR "universities" OR "higher education" OR "college$" OR
          (
            ("technic*" OR "vocation*" OR "tertiar*" OR "postsecondary" OR "post secondary")
            NEAR/3
            ("education" OR "training" OR "school*" OR "learning")
          ) OR
		  (
		  ("skill$" OR "job" OR "career" OR "workforce") NEAR/3 "training"
		  )
        )
      )
      OR
      (
        ("employ*" OR "job$" OR "work" OR "job access" OR "job creation" OR "labor market" OR "workforce" OR "carer development" OR "socioeconomic attainment$" OR "school-to-work transition$")
        NEAR/7
        ("youth*" OR "young people" OR "adolescen*" OR "teen*" OR "young adult*")
      )
    )
  )
)
```

### Target 8.7

> **8.7 Take immediate and effective measures to eradicate forced labour, end modern slavery and human trafficking and secure the prohibition and elimination of the worst forms of child labour, including recruitment and use of child soldiers, and by 2025 end child labour in all its forms**
>
> 8.7.1 Proportion and number of children aged 5‑17 years engaged in child labour, by sex and age

This target is interpreted to cover research about
* Eradication of forced labour, modern slavery and human trafficking
* prohibit and end child labour and child soldiers

The two steps for ending child labour is not considered essential, and the aspect of child soldiers is included in the interpretation as this is not always defined as child labour.

```py
TS=
(

)
```

### Target 8.8

> **8.8 Protect labour rights and promote safe and secure working environments for all workers, including migrant workers, in particular women migrants, and those in precarious employment**
>
> 8.8.1 Fatal and non-fatal occupational injuries per 100,000 workers, by sex and migrant status
>
> 8.8.2 Level of national compliance with labour rights (freedom of association and collective bargaining) based on International Labour Organization (ILO) textual sources and national legislation, by sex and migrant status

This target is interpreted to cover research about
* protecting labour rights
* promoting safe and secure working environments for all workers

The ILO definition of labour rights is "freedom of association and the effective recognition of the right to collective bargaining" <a href="#f8">(ILO, 2022a)</a>.

```py
TS=
(

)
```

### Target 8.9

> **8.9 By 2030, devise and implement policies to promote sustainable tourism that creates jobs and promotes local culture and products**
>
> 8.9.1 Tourism direct GDP as a proportion of total GDP and in growth rate

This target is interpreted to cover research about 

* implementing policies to promote sustainable tourism

This includes research on the environmental, economic and cultural dimensions of sustainable tourism (<a href="#f5">UN Tourism, 2025</a>). 

The UNWTO (<a href="#f8">2013</a>) defines sustainable tourism as:

> "Tourism that takes full account of its current and future economic, social and environmental impacts, addressing the needs of visitors, the industry, the environment, and host communities”.

Other aspects of sustainable tourism are also covered in SDG 12.b, which was also used as a basis for the phrases for this target.

The basic structure is *action + policies + sustainable tourism* and *action + policies + job creation/local culture + sustainable tourism*

```py
TS = 
(
  (
    (
      (
	    "develop" OR "development" OR "promote" OR "strengthen*" OR "improv*" OR "enhanc*" OR "increas*" OR "build$" OR "building" OR "built" OR "advance" OR "advancing" 
		OR "establish*" OR "consider*" OR "encourag*" OR "ensure" OR "implement" OR "adopt*" OR "apply" OR "enforce" OR "propose*" OR "design*" OR "plan" OR "planning" 
		OR "introduc*" OR "pathway$" OR "path$" OR "route" OR "roadmap" OR "towards"
      ) 
      NEAR/5
      (
        "policies*" OR "policy" OR "law$" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR "treaties" OR "strateg*" OR "framework$" OR "instrument$" 
		OR "governance" OR "rule" OR "rules" OR "procedur*" OR "practice$" OR "action$" OR "principle$" OR "initiative*"
      )
    )
    NEAR/15
    (
      "ecotourism" OR "eco-tourism" OR
      (
        (
          "sustainab*" OR "responsib*" OR "environmental*" OR "ecolog*" OR "eco" OR "green" OR "inclusive" OR "ethical" OR "fair" OR "conscious" OR "resilient" OR "regenerative"
        )
        NEAR/3
        (
          "tourism" OR "tourist$" OR "hospitality" OR "leisure" OR "ecotourism" OR "eco-tourism" OR "air travel" OR "airline travel" OR "air transport" OR "aviation" OR "flight*" OR
          "air passenger travel" OR "airport tourism" OR ("cruise" NEAR/5 ("travel" OR "tourism" OR "ship")) OR "hotel$"
        )
      )
	)
    OR
    (
      (
        "job creation" OR "employment" OR "livelihood$" OR "income generation" OR "entrepreneurship" OR "economic empowerment" OR "local economy" OR "local economies" OR "value chain$" OR
        "microenterprise$" OR "small business*" OR "community development$" OR "inclusive growth" OR "social inclusion" OR "cultural heritage" OR "local culture$" OR
        "indigenous knowledge" OR "traditional practice$"
      )
      NEAR/5
      (
        "ecotourism" OR "eco-tourism" OR
        (
          "sustainab* tourism" OR "responsib* tourism" OR "environmental* tourism" OR "ecological* tourism" OR "eco tourism" OR "green tourism" OR "inclusive tourism" OR "ethical tourism" OR "fair tourism" OR "conscious tourism" OR "resilient tourism" OR "regenerative tourism"
        )
      )
    )
  )
)
```

### Target 8.10

> **8.10 Strengthen the capacity of domestic financial institutions to encourage and expand access to banking, insurance and financial services for all**
>
> 8.10.1 (a) Number of commercial bank branches per 100,000 adults and (b) number of automated teller machines (ATMs) per 100,000 adults
>
> 8.10.2 Proportion of adults (15 years and older) with an account at a bank or other financial institution or with a mobile-money-service provider

This target is interpreted to cover research about 

* expanding access to financial services from local, domestic and/or national institutions
* enhancing financial inclusion through physical or digital infrastructure

This includes studies on barriers to financial access, especially for underserved populations, as well as efforts to improve institutional capacity, regulatory frameworks, and technological tools (e.g., mobile banking, fintech) to support inclusive economic participations.

This interpretation takes into account the two indicators with regards to both the physical infrastructure required for banks and ATMs, as well as digital infrastructure for mobile banking solutions.

```py
TS=
(

)
```

### Target 8.a

> **8.a Increase Aid for Trade support for developing countries, in particular least developed countries, including through the Enhanced Integrated Framework for Trade-Related Technical Assistance to Least Developed Countries**
>
> 8.a.1 Aid for Trade commitments and disbursements

This target is interpreted to cover research about 
* Increasing Aid for Trade support for developing countries

Aid for Trade is an initiative by the World Trade Organization about "helping developing countries, in particular the least developed, to build the trade capacity and infrastructure they need to benefit from trade opening." <a href="#f7">(WTO, n.d.)</a>

```py
TS=
(

)
```

### Target 8.b

> **8.b By 2020, develop and operationalize a global strategy for youth employment and implement the Global Jobs Pact of the International Labour Organization**
>
> 8.b.1 Existence of a developed and operationalized national strategy for youth employment, as a distinct strategy or as part of a national employment strategy

This target is interpreted to cover research about 

* developing and implementing youth employment strategies
* implementing the Global Jobs Pact

This includes research on the design, evaluation, and implementation of youth labor market policies and coordinated programs at national or multilateral levels. The Global Jobs Pact <a href="#f6">(ILO, 2022b)</a> is mentioned specifically, but the boarder aim is to capture institutional strategies for increasing youth employment, particularly within structured or policy-driven contexts.

```py
TS=
(

)
```


## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<a id="f4"></a>International Labour Organization. (2017). *Measuring productive employment: A 'how to' note*. https://www.ilo.org/sites/default/files/2024-05/wcms_565180.pdf [Accessed 2025.09.05]

<a id="f8"></a>International Labour Organization. (2022a). *ILO declaration on fundamental principles and rights at work and its follow-up: Adopted at the 86th session of the International Labour Conference (1998)
and amended at the 110th session (2022)*. https://www.ilo.org/sites/default/files/2024-04/ILO_1998_Declaration_EN.pdf

<a id="f6"></a>International Labour Organization. (2022b). *Recovering from the crisis: A Global Jobs Pact (adopted by the International Labour Conference in 2009 and amended in 2022)*. https://www.ilo.org/sites/default/files/wcmsp5/groups/public/%40ed_norm/%40relconf/documents/meetingdocument/wcms_115076.pdf [Accessed 2025.09.05]

<a id="f3"></a>International Labour Organization. (2025). *Decent work*. https://www.ilo.org/topics-and-sectors/decent-work [Accessed 2025.09.05]

<a id="f1"></a>UN DESA. (2025). *Goals: Ensure availability and sustainable management of water and sanitation for all*. https://sdgs.un.org/goals/goal8#targets_and_indicators [Accessed 2025.04.22]

<a id="f5"></a>UN Tourism. (2025). *Sustainable development*. https://www.untourism.int/sustainable-development [Accessed 2025.09.05]

<a id="f2"></a>United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

<a id="f8"></a>UNWTO (2013). *Sustainable Tourism for Development Guidebook - Enhancing capacities for Sustainable Tourism for development in developing countries*. https://www.e-unwto.org/doi/epdf/10.18111/9789284415496.

<a id="f7"></a>World Trade Organization. (n.d.). *Aid for Trade fact sheet*. https://www.wto.org/english/tratop_e/devel_e/a4t_e/a4t_factsheet_e.htm