# Search query for SDG 2 - Zero Hunger, Bergen action-approach.

End hunger, achieve food security and improved nutrition and promote sustainable agriculture.

**Current status**: This string is currently a finished version (1.0.0).

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes

## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here: https://www.webofscience.com/wos/woscc/summary/b3b8d55f-4112-42a3-9c12-de4dc95f8a76-55efa21b/relevance/1 (no filters, all years)

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 2 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 2 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021a](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f3)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

During editing of this string (2021), we have consulted two other sets of queries for reference: <a id="Aurora">[Aurora Universities network (2020)](#f5)</a> and <a id="Els">[Rivest et al. (2021)](#f6)</a>.

**Abbreviations**
* FAO - Food and Agriculture Organization of the United organizations
* WHO - World Health Organization
* MeSH - Medical Subject Headings - https://www.ncbi.nlm.nih.gov/mesh/

## 3. Targets

### Target 2.1

> **2.1 By 2030, end hunger and ensure access by all people, in particular the poor and people in vulnerable situations, including infants, to safe, nutritious and sufficient food all year round.**
>
> 2.1.1 Prevalence of undernourishment
>
> 2.1.2 Prevalence of moderate or severe food insecurity in the population, based on the Food Insecurity Experience Scale (FIES)

This target is interpreted to cover research about
* Ending/reducing hunger/lack of food, reducing food insecurity
* Increasing access to food and improving food supply systems
* Increasing the safety and nutritional value of the food available.

It consists of 3 phrases. Phrase 3 uses terms which need to be combined with human terms.

#### Phrase 1

The general structure is *hunger + action*

Hunger is used in phrases (`ending hunger`, `world hunger`) to prevent finding results that are mostly medical/physiological. `feast and famine` refers to bioreactors/selective pressure in microbial cultures (not relevant), and is used in a double NOT to avoid losing relevant results. `Underfeeding` and `starvation` removed as seem to be used mostly in a medical/physiology context, rather than related to food security/supply.

```py
TS=
(
  (
    ("end hunger" OR "ending hunger" OR "ends hunger" OR "world hunger"
    OR "hunger and poverty" OR "poverty and hunger" OR "famine$"
    OR "food insecurity" OR "nutritional insecurity"
    )
    NEAR/5
        (   "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting"
            OR "alleviat*" OR "tackl*" OR "combat*" OR "fight*"
            OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
            OR "prevent*" OR "avoid*"
            OR "manag*" OR "treat*" OR "therapy" OR "therapies" OR "intervention$"
            OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
        )
  )
  NOT (("feast and famine" OR "feast-famine") NOT ("end* hunger" OR "malnutrition"))    
)
```

#### Phrase 2

The general structure is *food access/safety/nutrition + action*. `food` should cover mechanisms such as food banks, food stamps, food credits, and descriptions such as good quality food etc. `nutrition* quality` does find some results about animal feed, but a number of them connect their work to food security, reducing food loss, so it is safer not to remove this term. Here we are including `food sovereignty` as it encompasses the ideas of access to safe, adequate and nutritious food, so is included here.

```py
TS=
(
  ("right to food" OR "right to adequate food" OR "food sovereignty"
  OR "nutrition* security" OR "nutrition* quality" OR "nutrition sensitive agriculture"
  OR
    ("food"
    NEAR/5
        ("access" OR "safety" OR "unsafe" OR "secure" OR "security"
        OR "reliable" OR "reliability"    
        )
    )
  )
  NEAR/5
     ("improv*" OR "enhanc*" OR "increas*" OR "strengthen" OR "attain" OR "achiev*"
     OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "manag*" OR "promote"
     OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
     )
)
```   

#### Phrase 3

The general structure is *food supply/value + action + humans*. 

This phrase covers improving food supply, and is combined with "human terms" to prevent biology/ecology results. The human terms include generic terms signifying a work is about humans as well as some "vulnerable" groups (based on UN sources) considered relevant for this topic (<a id="Blanchard">[Blanchard et al., 2017](#f16)</a>; <a id="UNOHC">[Office of the High Commissioner, n.d.](#f17)</a>). Note that `food supply` will also find works about the food supply chain etc. 

```py
TS=
 (
    (
      ("food supply" OR "nutritional value" OR "nutrient content" OR "nutritional content")
      NEAR/5
         ("improv*" OR "enhanc*" OR "increas*" OR "strengthen" OR "attain" OR "achiev*"
         OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "manag*"
         OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
         )
    )  
    AND
        ("humans" OR "humanity" OR "human" OR "people" OR "person$"
        OR "children" OR "child" OR "under fives" OR "infant$" OR "toddler$" OR "babies" OR "teenager$" OR "adolescent$" OR "youth$" OR "girls" OR "boys"
        OR "adult$" OR "women" OR "men" OR "woman" OR "man"
        OR "agricultur*" OR "food security" OR "poverty"
        OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
        OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
        OR "rural" OR "urban" OR "countr*" OR "nation$" OR "develop* state$"
        )
)
```

### Target 2.2

> **2.2 By 2030, end all forms of malnutrition, including achieving, by 2025, the internationally agreed targets on stunting and wasting in children under 5 years of age, and address the nutritional needs of adolescent girls, pregnant and lactating women and older persons.**
>
> 2.2.1 Prevalence of stunting (height for age less than -2 standard deviation from the median of the World Health Organization (WHO) Child Growth Standards) among children under 5 years of age
>
> 2.2.2 Prevalence of malnutrition (weight for height more than +2 or less than -2 standard deviation from the median of the WHO Child Growth Standards) among children under 5 years of age, by type (wasting and overweight)
>
> 2.2.3 Prevalence of anaemia in women aged 15 to 49 years, by pregnancy status (percentage)

This target is interpreted to cover research about reducing malnutrition and improving the nutritional status for all people (including elements specific to children, girls, the elderly and pregnant women). Malnutrition includes both underweight and overweight (<a id="WHOmalnut">[WHO, 2021](#f4)</a>); this WHO factsheet was used to add terms, including specific micronutrients of worldwide importance (iodine, iron, vitamin A).

This query consists of 3 phrases. Phrase 3 is for terms which need to be combined with human terms.

#### Phrase 1

The general structure is *malnutrition + action*

Actions such as `decreas*` will cover formulations such as "to reduce the risk of obesity". `dietary NEAR/3 deficiency` finds a number of specific deficiencies (e.g. dietary selenium deficiency, dietary Zn deficiency). `minerals` is not used - it only adds a few results, and many are from agriculture. `obese` is not included alone, as it tends to be used as a descriptor for a subject group, e.g. "reducing condition x in obese adults", rather than reducing obesity itself. `undernutrition` and other terms are included in phrase 3.

```py
TS=
(
  (
      ("malnutrition" OR "malnourish*"
      OR "kwashiorkor" OR "marasmus"
      OR "anaemia" OR "anemia"
      OR
        (
          ("deficien*" OR "inadequa*")
          NEAR/3
              ("nutritional" OR "dietary" OR "vitamin$" OR "micronutrient$" OR "iron" OR "iodine")
        )
      OR
        (
          ("stunting" OR "stunted" OR "wasting" OR "underweight")
          NEAR/15 ("child*" OR "infant$" OR "under five$" OR "babies" OR "toddler$" OR "girl$" OR "boy$")
        )
      OR "obesity" OR "overweight" OR "becoming obese"
      )
      NEAR/5
          ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting"
          OR "alleviat*" OR "tackl*" OR "combat*" OR "fight*"
          OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
          OR "prevent*" OR "avoid*"
          OR "manag*" OR "treat*" OR "therapy" OR "therapies" OR "intervention$"
          OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
          )
  )
  NOT ("salmon anemia")    
)
```

#### Phrase 2

The general structure is *nutritional access/quality/status of specific groups + action*

Research about improving the nutritional status of the groups mentioned in the target is included here. `stability` is not used in combination with food/nutrition as there are results about nutritional stability in processed foods. `nutritio*` should cover terms such as "access to nutritional care". `baby` is not used as it only adds noise about "baby mustard".

```py
TS=
(
  (
    ("nutritio*"
      NEAR/5 ("access" OR "safe" OR "unsafe" OR "secure" OR "reliable" OR "reliability")
    )
  OR "diet* quality" OR "nutrition* security" OR "nutrition* quality" OR "nutrition sensitive agriculture"
  OR
    (
      ("nutritio*" OR "folate status" OR "micronutrient$")
      NEAR/5
          ("women" OR "mother$" OR "pregnancy"
          OR "child*" OR "under five$" OR "infant$" OR "toddler$" OR "girl$" OR "boy$" OR "babies" OR "perinatal"
          OR "old* persons" OR "old* people" OR "elderly" OR "older adult$"
          )
    )
  )
  NEAR/5
     ("improv*" OR "enhanc*" OR "increas*" OR "strengthen" OR "attain" OR "achiev*"
     OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "manag*" OR "promote"
     OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
     )
)
```

#### Phrase 3

The general structure is *undernutrition/food supply + actions + humans*. For the topics `"protein deficiency"  OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition"` and `food supply` there was a considerable number of papers from animals and therefore they had to be combined with *human terms*. The human terms include generic terms signifying a work is about humans as well as some "vulnerable" groups (based on UN sources) considered relevant for this topic (<a id="Blanchard">[Blanchard et al., 2017](#f16)</a>; <a id="UNOHC">[Office of the High Commissioner, n.d.](#f17)</a>).

```py
TS=
(
  (
    (
      ("protein deficiency"
      OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition"
      )
      NEAR/5
          ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting"
           OR "alleviat*" OR "tackl*" OR "combat*" OR "fight*"
           OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
           OR "prevent*" OR "avoid*"
           OR "manag*" OR "treat*" OR "therapy" OR "therapies" OR "intervention$"
           OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
          )
    )
  )
  AND
      ("humans" OR "humanity" OR "human" OR "people" OR "person$"
      OR "children" OR "child" OR "under fives" OR "infant$" OR "toddler$" OR "babies" OR "teenager$" OR "adolescent$" OR "youth$" OR "girls" OR "boys"
      OR "adult$" OR "women" OR "men" OR "woman" OR "man"
      OR "agricultur*" OR "food security" OR "poverty"
      OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali$ed group" OR "marginali$ed groups" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
      OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
      OR "rural" OR "urban" OR "countr*" OR "nation$" OR "develop* state$"
      )
)
```

### Target 2.3

> **2.3 By 2030, double the agricultural productivity and incomes of small-scale food producers, in particular women, indigenous peoples, family farmers, pastoralists and fishers, including through secure and equal access to land, other productive resources and inputs, knowledge, financial services, markets and opportunities for value addition and non-farm employment.**
>
> 2.3.1 Volume of production per labour unit by classes of farming/pastoral/forestry enterprise size
>
> 2.3.2 Average income of small-scale food producers, by sex and indigenous status

This target is interpreted to include research about increasing the productivity and income of small-scale food producers (terrestrial and aquatic). Specific ways to do this are mentioned (securing access, rights, and opportunities for non-farm employment/value addition), so these are included too.

This query consists of 1 phrase. The basic structure is *productivity/access etc. + action + small-scale food producers*

 For the *small-scale food prodcer terms*, `small scale`+ `farm*` will cover types of farming in two words e.g. forest farming. Types of farming system were expanded using MeSH (NIH) and Emtree (Embase database, Elsevier) subject vocabularies. Specific types of crops and livestock were further expanded using FAO statistical year book (<a id="FAO2013">[FAO, 2013](#f2)</a>). For crops, those listed as major crops or "important food crops" are included, while oil crops were excluded (not being food). Adding different farming types/crops/livestock adds complexity but improves the results. Some specific types are covered by generic terms: e.g. Root crops are covered by `crops`, and terms such as `farm*` will cover types of farming in two words e.g. forest farms, family farms, fish farming.

 In the *productivity/access etc. terms*:
 - `intensification` implies increasing production, but results in some noise when used alone - it can be used in other contexts, and finds many results about the *effects* of agricultural intensification, thus it is combined with other terms which limit it better to works looking at the process itself.
- Originally `"access*" OR "barrier$"` was combined with many other terms (e.g. access to credit, financial services, markets...) - however we have now cut this combination, as the target is so broad in what should be accessible. So now, papers talking about improving access to anything should be covered. A few irrelevant results are included due to the abstract including an "open access" publishing statement; and a couple from open access to e.g. satellite data. This is hard to exclude as we want "open access fisheries", for example. (Original combination: `"farmland$" OR "land" OR "resources" OR "financial service$" OR "banking" OR "microfinance" OR "credit" OR "microcredit" OR "insurance" OR "microinsurance" OR "market$" OR "marketing" OR "traders" OR "trade" OR "agricultur* input$" OR "farm input$" OR "water" OR "machinery" OR "equipment" OR "technology" OR "farm* experience" OR "information" OR "training" OR "equitab*" OR "inequitab*"`)

```py
TS= (
      (
        ("intensification" NEAR/5 ("smallhold*" OR "sustainable" OR "agroecolog*" OR "ecolog*"))  
        OR
          (
            ("production" OR "productivity" OR "yield$" OR "agricultural output$" OR "farm output$"
            OR "livelihood$" OR "income$" OR "profit*" OR "revenue" OR "economic viability"
            OR "value addition" OR "diversification" OR "non-farm employment" OR "off-farm employment" OR "off farm income"
            OR "access*" OR "empowerment" OR "benefit$" OR "tenure"
            OR ("right$" NEAR/5 ("farmland$" OR "land" OR "property" OR "tenure"))
            OR "equity" OR "equitable" OR "justice" OR "injustice"
            )
            NEAR/5
                ("improv*" OR "increase" OR "increasing" OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
                OR "more efficie*" OR "better" OR "raise" OR "bolster" OR "strengthen*" OR "empower" OR "empowering"
                OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
                )
          )
        OR
          (
            ("barrier$" OR "obstacle$"
            OR "injustice"
            OR "land grab*" OR "tenure insecurity"
            )
            NEAR/5
                ("reduc*" OR "prevent*" OR "remov*" OR "fight*" OR "combat*"
                OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*" OR "regulate"
                )
          )
        )
        AND
          ("smallhold*" OR "family farm*" OR "family run farm*" OR "family owned farm*" OR "home gardening"
          OR
            (
              ("small-scale" OR "indigenous" OR "homestead*" OR "subsistence")
              NEAR/5
                (
                  ("food producer$" OR "food production" OR "food grower$" OR "agro food$"
                  OR "agricultur*" OR "farm*" OR "permaculture"
                  OR "cropping system$" OR "orchard$" OR "arable land$"
                  OR "pasture$" OR "pastoral*" OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
                  OR "aquaculture" OR "fisher*" OR "fish farm*"
                  )
                OR
                  (
                    ("crop$" OR "produce" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
                    OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
                    )
                    NEAR/5
                        ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding")
                  )
                )
            )
          )
)
```   

### Target 2.4

> **2.4 By 2030, ensure sustainable food production systems and implement resilient agricultural practices that increase productivity and production, that help maintain ecosystems, that strengthen capacity for adaptation to climate change, extreme weather, drought, flooding and other disasters and that progressively improve land and soil quality.**
>
> 2.4.1 Proportion of agricultural area under productive and sustainable agriculture

This target is interpreted to cover research about
* increasing the productivity of food production systems (phrase 1)
* implementation of resilient food production systems/agricultural practices, including strengthening adaptation and preparedness of food production systems/species to climate change and disasters (phrases 2,3)
* increasing sustainable food production systems/practices (outside of resilience; phrase 4)
* how food production systems can improve/maintain soil quality and ecosystems (phrase 5,6)

Increasing productivity of all food production systems (i.e. without reference to sustainable/resilient practices) was not considered relevant in v1. However, the SDG indicator metadata clearly classes increased productivity as part of sustainability. Thus, it is included now.
> "Maintaining or improving the output over time relative to the area of land used is an important aspect in  sustainability  for  a  range  of  reasons.  [...]. In a broader sense, an increase in the level of  land  productivity  enables  higher  production  while  reducing  pressure  on  increasingly  scarce  land  resources,  commonly  linked  to  deforestation  and  associated  losses  of  ecosystem  services  and biodiversity." (<a id="SDGindmetadata">[Statistics Division, 2021b, Indicator 2.4.1](#f9)</a>).

Under "food production systems" we include types of agriculture, fishing and aquaculture. We do not include processing, storage, distribution, and markets, which can be considered part of a wider "sustainable food system" (<a id="SFS">[e.g. Annex 2, Annex 3 in One Planet network Sustainable Food Systems (SFS) Programme, 2020](#f8)</a>). Thus concepts such as food sovereignty are too wide. Types of farming system were expanded using MeSH (NIH) and Emtree (Embase database, Elsevier) subject vocabularies. Specific types of crops and livestock were further expanded using FAO statistical year book (<a id="FAO2013">[FAO, 2013](#f2)</a>). For crops, those listed as major crops or "important food crops" are included, while oil crops were excluded (not being food). Some specific types are covered by generic terms: e.g. Root crops are covered by `crops`, and terms such as `farm*` will cover types of farming in two words e.g. forest farms, family farms, fish farming.

This query consists of 6 phrases.

#### Phrase 1

The general structure is *food production systems + production + action*. `intensification` implies increasing production, but results in some noise when used alone - it can be used in other contexts, and finds many results about the *effects* of agricultural intensification, thus it is combined with other terms which limit it better to works looking at the process itself.

```py
TS=
(
  (
      ("food production" OR "food grower$"
      OR "farm*" OR "agricultur*" OR "ecoagricultur*" OR "eco agricultur*" OR "permaculture"
      OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
      OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
      OR "aquaculture" OR "fish farm*"
      OR
        (
          ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
          OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
          )
          NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
        )      
      )
      NEAR/15
          (
            ("intensification"
            NEAR/5 ("sustainable" OR "agroecolog*" OR "ecolog*")
            )
          OR
            (
              ("production" OR "productivity" OR "efficiency" OR "yield$" OR "agricultural output$" OR "farm output$")
              NEAR/5
                ("improv*" OR "increas*" OR "enhanc*" OR "stimulat*"
                OR "more efficie*" OR "better" OR "raise" OR "bolster" OR "strengthen*"
                )
            )
          )  
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*")
)
```  

#### Phrase 2

Phrase 2 and 3 concern reducing vulnerability / increasing resilience. They have the same terms for food production systems, but differ in the terms for resilience: phrase 2 is linked to general terms for resilience, while phrase 3 covers terms that need to be connected to disasters/shocks/risks.

Resilience in terms of food production has been described by FAO as:
> " In the context of sustainable food and agriculture, resilience is the capacity of agro-ecosystems, farming communities, households or individuals to maintain or enhance system productivity by preventing, mitigating or coping with risks, adapting to change, and recovering from shocks" (<a id="FAO2014">[FAO, 2014, p.28](#f7)</a>)

The basic structure of phrase 2 is *food production systems + resilience/vulnerability + action*.

In the *food production system* terms, production systems and species are included (i.e. species are split from production where possible so that both resilience for the species and the production system will be covered). Some species remain linked to production to avoid irrelevant results (e.g. vegetable intake and psychological resilience). `pastoral*` is limited in this phrase, as it finds results from other uses (pastoral care, religion studies).

In the *resilience* terms, `tolera*` is a particularly influential term that increases results ("drought tolerance" of crops being a common research theme). `climate smart agriculture` is a term used for an approach specifically addressing climate change.

```py
TS=
(
  (
      ("food production" OR "food grower$" OR "agro food"
      OR "farm*" OR "agricultur*" OR "ecoagricultur*" OR "eco agricultur*" OR "permaculture"
      OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoralist$"
      OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
      OR "aquaculture" OR "fisher*" OR "fish farm*"
      OR "crop$" OR "cereal$" OR "rice" OR "wheat" OR "maize"
      OR "livestock" OR "cattle" OR "sheep" OR "poultry" OR "chicken$" OR "pig$" OR "goat$"
      OR
        (
          ("grain$" OR "vegetable$" OR "fruit$" OR "pulses" OR "fish" OR "buffalo*" OR "duck$")
          NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
        )      
      )
      NEAR/15
          (
            (
              ("climate smart agriculture" OR "resilien*"
              OR (("disaster$" OR "risk$") NEAR/3 ("plan*" OR "strateg*" OR "relief" OR "manag*"))
              )
              NEAR/5
                  ("adopt*" OR "apply" OR "implement*" OR "establish*" OR "build*" OR "create" OR "creating"
                  OR "improv*" OR "increase" OR "increasing" OR "maintain*"
                  OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "strengthen*" OR "empower" OR "empowering"
                  OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
                  OR "adaptation fund" OR "climate financ*" OR "climate aid" OR "green climate fund" OR "least developed countries fund"
                  )
            )
            OR
              ("vulnerability"
              NEAR/5
                ("reduc*" OR "decreas*" OR "prevent*" OR "remov*" OR "fight*" OR "combat*"
                OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
                )
              )
          )  
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*" OR "wild pig$")
)
```  

#### Phrase 3

The basic structure of phrase 3 is *food production systems + adaptation/coping/preparedness + action + disaster/climate change*.

The *food production system* terms are the same as phrase 2.  These *disaster/climate change* terms include natural disasters, climate, market volatility, civil and political unrest (examples of risks in <a id="FAO2014">[FAO, 2014](#f7)</a>).

The *disaster* terms were taken from a standardised list we used across the SDGs, which was developed based on selected hazards listed in <a id="Murray">[Murray et al. (2021)](#f15)</a>.

```py
TS=
(
  (
    ("food production" OR "food grower$" OR "agro food"
    OR "farm*" OR "agricultur*" OR "ecoagricultur*" OR "eco agricultur*" OR "permaculture"
    OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoralist$"
    OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
    OR "aquaculture" OR "fisher*" OR "fish farm*"
    OR "crop$" OR "cereal$" OR "rice" OR "wheat" OR "maize"
    OR "livestock" OR "cattle" OR "sheep" OR "poultry" OR "chicken$" OR "pig$" OR "goat$"
    OR
      (
        ("grain$" OR "vegetable$" OR "fruit$" OR "pulses" OR "fish" OR "buffalo*" OR "duck$")
        NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
      )      
    )
    NEAR/15
      (
        ("adapt*" OR "mitigat*" OR "protect*" OR "avoid*" OR "limit" OR "prevent*"
        OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
        OR
          (
            ("cope" OR "coping" OR "tolera*" OR "preparedness" OR "early warning")
            NEAR/5
              ("implement*" OR "establish*" OR "build*" OR "develop"
              OR "improv*" OR "increase" OR "increasing" OR "maintain*"
              OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "strengthen*"
              )
          )
        )
        NEAR/5
            ("climate change" OR "climatic change$" OR "global warming" OR "changing climate"
            OR "disaster$" OR "catastroph*"
            OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
            OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
            OR "drought$" OR "flood*"
            OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
            OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
            OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
            OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
            OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
            OR "tipping point$"  
            OR "outbreak$" OR "pandemic$" OR "epidemic$"
            OR "war" OR "wars" OR "armed conflict$"
            OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
            OR "financial crash*" OR "financial shock$" OR "financial disaster$"
            OR "economic downturn$" OR "economic shock$" OR "economic disaster$"
            )
      )
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*" OR "wild pig$")
)
```

#### Phrase 4

The general structure is *(ecoagriculture + action) OR (food production systems + sustainability + action)*.

`ecoagricultur*` is a relatively specialist term for ecology and agriculture and considered narrow enough to use alone.

Other terms suggesting research about sustainable agriculture were combined with the agricultural terms. `agroecolog*` (agroecology, or the agroecological approach) is considered a relevant term for sustainable, being related to ecology and environmental stability as well as social and cultural dimensions (<a id="SFS">[One Planet network Sustainable Food Systems (SFS) Programme, 2020, p. 28](#f8)</a>). Other terms for practices/approaches that can be considered to contribute to "sustainable food production systems" were gathered from <a id="HLPE">[High Level Panel of Experts on Food Security and Nutrition (2019, Appendix 1 and p. 36)](#f14)</a>; some of these also are relevant for soil quality. Other terms from this source are included in other phrases: "sustainable intensification" is covered in phrase 1, "climate smart agriculture" in phrase 2. `organic` must be combined due to use in other contexts (e.g. soil organic matter, organic carbon).

```py
TS=
  (
    ("ecoagricultur*" OR "eco-agricultur*" OR "permaculture"
    OR "conservation agriculture" OR "conservation farming"
    )
    NEAR/5
        ("adopt*" OR "apply" OR "implement*" OR "establish*" OR "build*"
        OR "improv*" OR "increase" OR "increasing" OR "maintain*"
        OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "strengthen*" OR "empower" OR "empowering"
        OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
        )
  )
OR
TS=
(
  (
    ("food production" OR "food grower$" OR "agri food"
    OR "farm*" OR "agricultur*"
    OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
    OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
    OR "aquaculture" OR "fisher*" OR "fish farm*"
    OR
      (
        ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
        OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
        )
        NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
      )      
    )
    NEAR/15
        (
          ("sustainab*" OR "agroecolog*" OR "eco-friendly" OR "environmentally friendly" OR "ecosystem approach"
          OR ("organic" NEAR/3 ("farm*" OR "agricultur*" OR "cultivation" OR "gardening" OR "production" OR "orchard$" OR "pasture$" OR "aquaculture"))
          OR "natural pest control" OR "natural pest management" OR "biological pest control" OR "intergrated pest management"
          OR "intercropping" OR "cover crop$" OR "crop rotation" OR "polyculture$" OR "permaculture"
          OR "reduced tillage" OR "mulch" OR "mulching"
          OR "water conservation"       
          )
          NEAR/5
              ("adopt*" OR "apply" OR "implement*" OR "establish*" OR "build*"
              OR "improv*" OR "increase" OR "increasing" OR "maintain*"
              OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "strengthen*" OR "empower" OR "empowering"
              OR  "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
              )
        )   
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*")  
)
```

#### Phrase 5

The general structure is *food production systems + ecosystems and soil + action*. This phrase covers "positives" (soil health, diversity, fertility etc.), phrase 6 covers "negatives" (loss, degradation etc.). Some terms are already covered in phrase 4 (e.g. reduced tillage).

```py
TS=
(
    ("food production" OR "food grower$" OR "agri food"
    OR "farm*" OR "agricultur*" OR "permaculture"
    OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
    OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
    OR "aquaculture" OR "fisher*" OR "fish farm*"
    OR
      (
        ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
        OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
        )
        NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
      )      
    )
    NEAR/15
          ("soil conservation"
          OR
            (
              ("soil structure" OR "soil fertility" OR "soil health"
              OR ("quality" NEAR/5 ("soil" OR "land" OR "farmland"))
              OR "biodiversity" OR "agrobiodiversity" OR "species diversity" OR "ecosystem$" OR "pollinator$"
              )
              NEAR/5
                ("improv*" OR "restor*" OR "enhanc*" OR "strengthen*"
                OR "maintain*" OR "preserv*" OR "conserv*" OR "protect*"
                OR "resilien*" OR "support"
                )
            )
          )     
)
```

#### Phrase 6

The general structure is *food production systems + ecosystems and soil + action*. This phrase covers "negatives" (loss, degradation etc.), phrase 5 covers "positives" (soil health, diversity, fertility etc.). Some terms are already covered in phrase 4 (e.g. reduced tillage).

Types of land/soil degradation are taken from <a id="FAO2014">[FAO (2014)](#f7)</a> and (<a id="SDGindmetadata">[Statistics Division, 2021b (Indicator 2.4.1)](#f9)</a>).

```py
TS=
(
  ("food production" OR "food grower$" OR "agri food"
  OR "farm*" OR "agricultur*" OR "permaculture"
  OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
  OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
  OR "aquaculture" OR "fisher*" OR "fish farm*"
  OR   
    (
      ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
      OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
      )
      NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
    )      
  )
  NEAR/15
      (
        ("desertification"
        OR
          ("soil$"
          NEAR/5
              ("loss" OR "degradation" OR "depletion" OR "nutrient imbalance$"
              OR "erosion" OR "compaction" OR "waterlogging"
              OR "salinization" OR "salinisation" OR "acidification"
              OR "chemical pollution" OR "contamination"
              )
          )
        OR
          (
            ("ecosystem$" OR "biodiversity" OR "land" OR "species" OR "pollinator$")
            NEAR/5 ("loss" OR "degradation" OR "depletion")
          )
        )
        NEAR/5
            ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "mitigat*"
            OR "lowering" OR "lower$" OR "lowered" OR "combat*"
            OR "stop*" OR "end" OR "ending" OR "halt"
            OR "avoid*" OR "prevent*"
            )
      )  
)
```  

### Target 2.5

> **2.5 By 2020, maintain the genetic diversity of seeds, cultivated plants and farmed and domesticated animals and their related wild species, including through soundly managed and diversified seed and plant banks at the national, regional and international levels, and promote access to and fair and equitable sharing of benefits arising from the utilization of genetic resources and associated traditional knowledge, as internationally agreed.**
>
> 2.5.1 Number of (a) plant and (b) animal genetic resources for food and agriculture secured in either medium- or long-term conservation facilities
>
> 2.5.2 Proportion of local breeds classified as being at risk of extinction

This target is interpreted to cover research about:
* The preservation of diversity of farmed species/wild relatives (phrases 1,2).
* Agricultural genetic banks and preservation of tissue (seed, plant, animal) related to conservation (phrase 3).
* Promoting access and benefit sharing for genetic resources and traditional knowledge related to food and agriculture (phrases 4,5).

The FAO Second Global Assessment of Animal Genetic Resources was used as a source of terms (<a id="FAO2015">[Commission on Genetic Resources for Food and Agriculture Assessments, 2015](#f11)</a>). Central instruments are The Treaty on Plant Genetic Resources for Food and Agriculture, the Convention on Biological Diversity and elaborations in the Nagoya Protocol.

Types of farming system were expanded using MeSH (NIH) and Emtree (Embase database, Elsevier) subject vocabularies. Specific types of crops and livestock were further expanded using FAO statistical year book (<a id="FAO2013">[FAO, 2013](#f2)</a>). For crops, those listed as major crops or "important food crops" are included, while oil crops were excluded (not being food). Some specific types are covered by generic terms: e.g. Root crops are covered by `crops`, and terms such as `farm*` will cover types of farming in two words e.g. forest farms, family farms, fish farming.

This query consists of 5 phrases.

#### Phrase 1

The general structure is *agricultural diversity/landraces/local breeds + action* - this phrase covers terms which are used in the context of agricultural diversity. Phrase 2 expands with generic terms for diversity that must be combined with agricultural terms.

Conserving wild relatives and traditional varieties is considered maintaining genetic diversity. `agrobiodiversity` is wider than only the species used in agriculture - it covers also the non-harvested species that support production and agro-ecosystems (e.g. pollinators, soil-organisms) (<a id="FAO2004">[FAO, 2004](#f10)</a>). It is considered relevant and included, as agrobiodiversity looks at the whole system (i.e. supporting diversity AND agricultural diversity). `conserv*` will cover e.g. conservation breeding, on-farm conservation etc. Note that `pigs` are excluded from the species list due to a large number of results about wild pig hunting in relation to their effect on agricultural land. 

```py
TS=
(
    ("agricultural diversity" OR "agricultural biodiversity" OR "agrobiodiversity"
    OR "landrace$" OR "wild relative$"
    OR  
      (
        ("local" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
        NEAR/1 
          ("breed$" OR "variet*" OR "cultivar$" 
          OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
          OR "livestock" OR "poultry" OR "cattle" OR "sheep" OR "goat$" OR "chicken$" OR "duck$" OR "buffalo*"
          )
      )
    OR "plant genetic resource$" OR "animal genetic resource$"
    )
    NEAR/5
        ("maintain*" OR "conserv*" OR "preserv*" OR "protect*"
        OR "Convention on biological diversity"
        OR
          (
            ("loss" OR "extinction" OR "declin*" OR "disappear*")
            NEAR/5
              ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "mitigat*"
              OR "lowering" OR "lower$" OR "lowered" OR "combat*"
              OR "stop*" OR "end" OR "ending" OR "halt"
              OR "avoid*" OR "prevent*"
              )
          )
        )        
)
```

#### Phrase 2

The general structure is *diversity + action + agriculture* - this phrase covers diversity terms which can be used outside the context of agricultural diversity. Complement to phrase 1.

Publications about groups and using terms which also include wild species (e.g. agricultural "seeds", cultivated "plants", farmed "fish") should be fdound by their use of `"agricultur*" OR "domestic*" OR "farming" OR "farm$" OR "farmed" OR "farmer$" OR "cultiva*"`.

Terminology to do with breeding programmes could be included here, but we want research that is about programmes for genetic diversity, and this should already be covered by *diversity + action* - the inclusion of breeding programmes alone finds results about programmes for other objectives (e.g. increased productivity). It also introduces noise around the *use* of genetic resources *for* breeding programmes, whereas we want research about breeding programs *for* genetic diversity. `conserv*` will cover e.g. conservation breeding, on-farm conservation etc..

```py
TS=
(
        ("increase genetic diversity" OR "improve genetic diversity"
        OR
          (       
             ("genetic diversity" OR "genetic resource$")
             NEAR/10
                  ("maintain*" OR "conserv*" OR "preserv*" OR "protect*" OR "secure" OR "securing"
                  OR
                      (
                        ("loss" OR "extinction" OR "declin*" OR "disappear*")
                        NEAR/5
                          ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "mitigat*"
                          OR "lowering" OR "lower$" OR "lowered" OR "combat*"
                          OR "stop*" OR "end" OR "ending" OR "halt"
                          OR "avoid*" OR "prevent*"
                          )
                      )
                  )
          )
        )
        NEAR/15
            ("agricultur*" OR "domestic*" OR "farming" OR "farm$" OR "farmer$" OR "cultiva*" OR "permaculture"
            OR "cropping system$" OR "orchard$"
            OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
            OR "aquaculture"
            OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
            OR "livestock" OR "poultry" OR "cattle" OR "sheep" OR "pig$" OR "goat$" OR "chicken$" OR "duck$" OR "buffalo*"      
            OR "landrace$" OR "wild relative$"
            OR
              (
                ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
                NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
              )
            )
)
```

#### Phrase 3

The general structure is *gene banks/ex situ + diversity/protection/policy + agriculture*

The *diversity/protection/policy* terms are included to help to filter out publications which mention genebanks that were used in research (i.e. samples were taken from...). They ensure that the work relates to conservation, genetic diversity, or gene bank policies in some way. Action terms are not used because multiple angles can be relevant - research about establishment of gene banks for maintaining diversity, research about farmers' use of gene banks, research about how best to store samples in gene banks, etc.

For the *gene bank/ex situ* terms, `cryoconservation` and `cryopreservation` are included as in vitro methods of conservation of diversity (<a id="FAO2015">[Commission on Genetic Resources for Food and Agriculture Assessments, 2015](#f11)</a>). For the *agriculture terms*, `domestic*` was removed from this phrase as results were mostly about domestic cats. A `NOT` expression was added for `seed banks` as these can be both human storage of seeds but also natural seed banks in the soil.

```py
TS=
(
  (
      ("cryoconservation"
      OR
        (
          ("plant bank$" OR "seed bank$"
          OR "gene bank$" OR "genebank$" OR "germplasm bank$" OR "cryobank$"
          OR "ex situ" OR "cryopreserv*"
          )
          NEAR/15
              ("diversity" OR "genetic resources" OR "agricultural biodiversity"
              OR "maintain*" OR "conserv*" OR "preserv*" OR "protect*" OR "extinct*" OR "endangered"
              OR "collection$ management" OR "collection$ development"
              OR "funding" OR "fund" OR "invest" OR "investing" OR "investment$"
              OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
              )
        )
      )  
      NEAR/15
          ("agricultur*" OR "farming" OR "farm$" OR "farmer$" OR "cultiva*" OR "permaculture"
          OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$"
          OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
          OR "aquaculture"
          OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
          OR "livestock" OR "poultry" OR "cattle" OR "sheep" OR "pig$" OR "goat$" OR "chicken$" OR "duck$" OR "buffalo*"     
          OR "landrace$" OR "wild relative$"
          OR
            (
              ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
              NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
            )
          )
  ) NOT ("soil seed bank$" OR "weed seed bank$" OR "dung seed bank$")        
)
```

#### Phrase 4

The general structure is *resources/knowledge + sharing/access + action + agriculture/food*.

For the *resource/knowledge* terms, `traditional NEAR knowledge` etc. will cover variations such as "traditional agricultural knowledge". The string is set up so that we do not have to define the benefits. Within the CBD/Nagoya protocol, benefits can be monetary/non-monetary (e.g. research results, royalties), related to using/commercialisation of genetic resources. "Using" includes research on genetics/biochemistry, development and biotechnology. (<a id="Garforth">[Garforth, 2018, p.3](#f12)</a>).

In the *sharing/access* terms, the more generic terms are combined with actions (e.g. increase access) while terms that are more specific to this issues are not (e.g. governance, justice), because it might be unnatural to write about e.g. "increasing justice". `access OR accessing OR accessib*` is used here to prevent "accessions". `biopiracy` is the unfair exploitation of biological resources/traditional knowledge.


```py
TS=
(
  (
    ("genetic resource$" OR "agrobiodiversity"
    OR "plant bank$" OR "seed bank$" OR "gene bank$" OR "genebank$" OR "germplasm bank$"
    OR "cryobank$" OR "ex situ" OR "cryopreserv*" OR "germplasm"
    OR "seed commons"
    OR "bioprospecting"
    OR (("traditional" OR "indigenous" OR "autochthonous") NEAR/3 ("knowledge"))
    )
    NEAR/15
        ("governance" OR "justice" OR "ownership"
        OR "biopiracy" OR "inequitable" OR "inequity"
        OR "material transfer agreement$" OR "informed consent"
        OR
          (
            ("sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$")
            NEAR/5
                ("improv*" OR "increase" OR "increasing" OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
                OR "better" OR "strengthen*" OR "empower" OR "empowering"
                OR "barrier$" OR "obstacle$"
                OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
                )
          )
        )
  )    
  AND
      ("food"
      OR "agricultur*" OR "domestic*" OR "farming" OR "farm$" OR "farmer$" OR "cultivar$" OR "permaculture"
      OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$"
      OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
      OR "aquaculture"
      OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
      OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
      OR "landrace$" OR "wild relative$"
      OR
        (
          ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
          NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
        )
      )                 
)   
```

#### Phrase 5

Phrase 5 is similar to phrase 4, with a focus on research that mentions instruments/treaties related to benefit sharing/access of genetic resources and traditional knowledge. The general structure is *resources/knowledge/rights + agriculture/food + instruments/specific issues*. Note that generic action terms are not included - we assume that works mentioning specific policy instruments are likely action-oriented. 

In this phrase, "rights" was added to `traditional NEAR knowledge` as this worked well with the combination with specific policy instruments.

```py
TS =
(
    ("genetic resource$" OR "agrobiodiversity"
    OR "bioprospecting"
    OR (("traditional" OR "indigenous" OR "autochthonous") NEAR/3 ("knowledge" OR "right$"))
    )
    AND
        ("food"
        OR "agricultur*" OR "domestic*" OR "farming" OR "farm$" OR "farmer$" OR "cultiva*" OR "permaculture"
        OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$"
        OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
        OR "aquaculture"
        OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
        OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
        OR "landrace$" OR "wild relative$"
        OR
          (
            ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
            NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
          )
        )
    AND
        ("Convention on biological diversity" OR "CBD"
        OR "Nagoya Protocol"
        OR "International Seed Treaty"
        OR "biopiracy"
        OR "Global Plan of Action for Animal Genetic Resources"
        OR "Plant Genetic Resources for Food and Agriculture" OR "PGRFA"
        )
)
```

### Target 2.a

> **2.a Increase investment, including through enhanced international cooperation, in rural infrastructure, agricultural research and extension services, technology development and plant and livestock gene banks in order to enhance agricultural productive capacity in developing countries, in particular least developed countries.**
>
> 2.a.1 The agriculture orientation index for government expenditures
>
> 2.a.2 Total official flows (official development assistance plus other official flows) to the agriculture sector

This target is interpreted to cover research about investment and international collaboration in rural infrastructure, agricultural research & technology, and gene banks in developing countries.

This query consists of 1 phrase. The general structure is *investment/cooperation + rural infrastructure/technology*. Note that this phrase does not contain an action element as it was considered too difficult/restrictive.

```py
TS =
(
      ("Agriculture Orientation Index for Government Expenditure$"
      OR
        (
          (
            ("government" OR "public")
            NEAR/3 ("expenditure" OR "invest*" OR "financ*" OR "spending")
          )
        OR "ODA" OR "cooperation fund$" OR "development spending"
        OR
          (
            ("international" OR "development" OR "foreign")
            NEAR/3
                ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
                OR "aid" OR "assistance" OR "fund$" OR "funding" OR "financing" OR "finance" OR "grant$" OR "investment$" OR "financial support" OR "financial resources"
                )
          )
        )
        NEAR/15
            ("rural infrastructure"
            OR "agronom*" OR "agroecolog*" OR "agro ecolog*" OR "agricultural sector"
            OR "plant bank$" OR "seed bank$" OR "gene bank$" OR "genebank$" OR "germplasm bank$" OR "cryobank$"
            OR
              (
                ("infrastructure" OR "technolog*" OR "biotech*" OR "research" OR "science$" OR "innovation" OR "R&D")
                NEAR/3 ("agricultur*" OR "farm*" OR "irrigation" OR "agri food" OR "agrifood")
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
      OR  "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR  "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      OR  "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
      OR   "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR "georgian*"
      )
)
```

### Target 2.b

> **2.b Correct and prevent trade restrictions and distortions in world agricultural markets, including through the parallel elimination of all forms of agricultural export subsidies and all export measures with equivalent effect, in accordance with the mandate of the Doha Development Round.**
>
> 2.b.1 Agricultural export subsidies

This target is interpreted to cover research about export subsidies (and equivalents) for agricultural/food exports, and trade restrictions and distortions for world agricultural/food markets. A WTO agricultural export subsidy fact sheet (<a id="WTOexport">[Information and External Relations Division of the WTO Secretariat, n.d.](#f13)</a>) was used as a source of terms, where food aid is also a factor.

This query consists of 2 phrases. Note that these phrases do not contain an action element as it was considered too difficult/restrictive.

#### Phrase 1

The basic structure is *export subsidies + agriculture/food*.

```py
TS=
(
  ("export subsid*" OR "export credit$" OR "export financ*" OR "export competition" OR "export support$")
  AND ("agricultur*" OR "agrifood" OR "food")
)
```

#### Phrase 2

The basic structure is *distortions + agricultural markets/exports*. Specific animals are not included due to results about restrictions in trade due to outbreaks of disease.

```py
TS=
(
  ("distort*" OR "price-fixing" OR "dumping"
  OR "trade restrict*" OR "Doha" OR "food aid"
  OR "state support*" OR "state financial support"
  OR "WTO dispute$"
  )
  NEAR/15
      (
        ("trade" OR "trading" OR "market$" OR "export$")
        NEAR/5 ("agricultur*" OR "agrifood" OR "food" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses")
      )
)
```

### Target 2.c

> **2.c Adopt measures to ensure the proper functioning of food commodity markets and their derivatives and facilitate timely access to market information, including on food reserves, in order to help limit extreme food price volatility.**
>
> 2.c.1 Indicator of food price anomalies

This target is interpreted to cover research about preventing price volatility in food/agriculture, and about ensuring stable food commodity markets. The basic structure is *action + volatility/stability + agricultural markets/prices*.

#### Phrase 1

```py
TS=
(
  (
    (
      ("prevent*" OR "avoid" OR "limit" OR "reduc*" OR "minimi*" OR "mitigat*" OR "tackl*" OR "combat"
      OR "stabiliz*" OR "stabilis*" OR "intervention$" OR "counteract"
      OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*" OR "regulat*"
      )
      NEAR/5 ("volatil*" OR "instability" OR "unstable" OR "anomalies" OR "price shock$" OR "price spike$" OR "inflation")
    )
  OR
    (
      ("improv*" OR "increase" OR "increasing" OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*"
      OR "secure" OR "securing" OR "ensur*" OR "maintain*" OR "strengthen*"
      )
      NEAR/5 ("stability" OR "stable" OR "functioning")
    )
  OR (("stabiliz*" OR "stabilis*") NEAR/5 ("price$" OR "market$"))
  )
  NEAR/15
        (
          ("price$" OR "market$")
          NEAR/5
            ("agricultur*" OR "agrifood" OR "food" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock")
        )
)
```

## 4. Contributions

* v2019.12: Marta Lorenz, Caroline S. Armitage, Susanne Mikki

* v1.0.0 Caroline S. Armitage (Oct 2021-Oct 2022)

* Internal review: Eli Heldaas Seland, Marta Lorenz (March 2022)

Specialist input: Awaiting specialist input.

## 5. Footnotes

<a id="f5"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f16"></a> Blanchard et al. (2017). *Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment*. United Nations Office for Disaster Risk Reduction. https://www.undrr.org/publication/marginalized-and-minority-groups-consideration-ndra. [↩](#Blanchard)

<a id="f11"></a> Commission on Genetic Resources for Food and Agriculture Assessments. (2015). *The Second Report on the State of the World’s Animal Genetic Resources for Food and Agriculture*. FAO. https://www.fao.org/publications/sowangr/en/

<a id="f10"></a> FAO. (2004). *What is Agrobiodiversity?* in "Building on Gender, Agrobiodiversity and Local Knowledge" [Training manual]. https://www.fao.org/3/y5609e/y5609e.pdf [↩](#FAO2004)

<a id="f2"></a> FAO statistical year book. (2013). *Part 3 Feeding the world*. ISBN: 9789251073964. http://www.fao.org/publications/card/en/c/1d6e6a08-4937-5c7d-8665-3e0ed6f29244

<a id="f7"></a> FAO. (2014). *Building a Common Vision for Sustainable Food and Agriculture. Principles and Approaches*. https://www.fao.org/3/a-i3940e.pdf [↩](#FAO2014)

<a id="f12"></a> Garforth, C. (2018). "An Introduction to the Nagoya Protocol on Access to Genetic Resources and the Fair and Equitable Sharing of Benefits Arising from their Utilization" in *Proceedings of the International Workshop on Access and Benefit-sharing for Genetic Resources for Food and Agriculture*. FAO. https://www.fao.org/3/CA0099EN/ca0099en.pdf [↩](#Garforth)

<a id="f14"></a> High Level Panel of Experts on Food Security and Nutrition. (2019). *Agroecological and other innovative approaches for sustainable agriculture and food systems that enhance food security and nutrition*. A report by the High Level Panel of Experts on Food Security and Nutrition
of the UN Committee on World Food Security, Rome. https://www.fao.org/cfs/cfs-hlpe/hlpe-reports/report-14-elaboration-process/en/ [accessed 03 Jan 2022] [↩](#HLPE)

<a id="f15"></a> Murray, V. et al. (2021) Hazard Information Profiles: Supplement to UNDRR-ISC Hazard Definition & Classification Review: Technical Report: Geneva, Switzerland, United Nations Office for Disaster Risk Reduction; Paris, France, International Science Council. DOI: 10.24948/2021.05 (https://council.science/publications/hazard-information-profiles/). [↩](#Murray)

<a id="f17"></a> Office of the High Commissioner (n.d.) *Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health*. United Nations Human Rights. https://www.ohchr.org/en/special-procedures/sr-health/non-discrimination-groups-vulnerable-situations (accessed Jun 2022). [↩](#UNOHC)

<a id="f8"></a> One Planet network Sustainable Food Systems (SFS) Programme. (2020). *Towards a Common Understanding of Sustainable Food Systems. Key approaches, concepts, and terms*. https://www.oneplanetnetwork.org/knowledge-centre/resources/towards-common-understanding-sustainable-food-systems-key-approaches [↩](#SFS)

<a id="f6"></a> Rivest, Maxime; Kashnitsky, Yury; Bédard-Vallée, Alexandre; Campbell, David; Khayat, Paul; Labrosse, Isabelle; Pinheiro, Henrique; Provençal, Simon; Roberge, Guillaume; James, Chris. (2021). *Improving the Scopus and Aurora queries to identify research that supports the United Nations Sustainable Development Goals (SDGs) 2021* V3. [Dataset]. doi: 10.17632/9sxdykm8s4.3 [↩](#Els)

<a id="f1"></a> Statistics Division. (2021a). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f9"></a> Statistics Division. (2021b). *SDG Indicators Metadata Repository*. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/metadata/ [accessed 8 December 2021] [↩](#SDGindmetadata)

<a id="f3"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/ [↩](#UNLDCs)

<a id="f4"></a> WHO. (2021, June 9). *Malnutrition*. [Fact sheet]. https://www.who.int/news-room/fact-sheets/detail/malnutrition. [↩](#WHOmalnut)

<a id="f13"></a> Information and External Relations Division of the WTO Secretariat. (n.d.). *Export subsidies and other export support measures* [Fact sheet]. World Trade Organization. https://www.wto.org/english/tratop_e/agric_e/factsheetagric17_e.htm [accessed 31 Dec 2021] [↩](#WTOexport)
