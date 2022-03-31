# Search query for SDG 2 - Zero Hunger, Bergen action-approach.

End hunger, achieve food security and improved nutrition and promote sustainable agriculture.

**Current status**: This string has undergone development to improve the phrases and structure, and is awaiting a review of these changes. It is substantially changed from the original version it was based on (v2019.11).

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 2
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes

## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG2</summary>

```
```

</details>

## 2. General notes

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021a](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f3)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

During editing of this string (2021), we have consulted two other sets of queries for reference: <a id="Aurora">[Aurora Universities network (2020)](#f5)</a> and <a id="Els">[Rivest et al. (2021)](#f6)</a>.

**Abbreviations**
* FAO - Food and Agriculture Organization of the United organizations
* WHO - World Health Organization
* MeSH - Medical Subject Headings - https://www.ncbi.nlm.nih.gov/mesh/

## 3. Targets

## Target 2.1

> **2.1 By 2030, end hunger and ensure access by all people, in particular the poor and people in vulnerable situations, including infants, to safe, nutritious and sufficient food all year round.**
>
> 2.1.1 Prevalence of undernourishment
>
> 2.1.2 Prevalence of moderate or severe food insecurity in the population, based on the Food Insecurity Experience Scale (FIES)

This target is interpreted to cover research about
* Ending/reducing hunger/lack of food, reducing food insecurity
* Increasing access to food and improving food supply systems
* Increasing the safety and nutritional value of the food available.

It consists of 3 phrases. Phrase 1 focuses on positive actions, phrase 2 on negative actions, and phrase 3 on terms which need to be combined with human terms.

#### Phrase 1

The general structure is *hunger + action*

Hunger is used in phrases (`ending hunger`, `world hunger`) to prevent finding results that are mostly medical/physiological. `feast and famine` refers to bioreactors/selective pressure in microbial cultures (not relevant), and is used in a double NOT to avoid losing relevant results. `Underfeeding` and `starvation` removed as seem to be used mostly in a medical/physiology context, rather than related to food security/supply.

```Ceylon =
TS=
(
  (
      ("end hunger" OR "ending hunger" OR "ends hunger" OR "world hunger" OR "hunger and poverty" OR "poverty and hunger"
      OR "famine$"
      OR "food insecurity"
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

``` Ceylon =
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

The general structure is *food supply + action + humans*. This phrase covers improving food supply, and is combined with "human terms" to prevent biology/ecology results.

``` Ceylon =
TS=
 (
    ("food supply"
      NEAR/5
         ("improv*" OR "enhanc*" OR "increas*" OR "strengthen" OR "attain" OR "achiev*"
         OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "manag*"
         OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
         )
    )  
    AND
        ("humans" OR "humanity" OR "human" OR "people" OR "person$"
        OR "children" OR "child" OR "under fives" OR "infant$" OR "babies" OR "adolescent$" OR "adult$"
        OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys"
        OR "agricultur*" OR "food security" OR "poverty"
        OR "rural" OR "urban" OR "countr*" OR "nation$" OR "develop* state$"
        )
)
```

## Target 2.2

> **2.2 By 2030, end all forms of malnutrition, including achieving, by 2025, the internationally agreed targets on stunting and wasting in children under 5 years of age, and address the nutritional needs of adolescent girls, pregnant and lactating women and older persons.**
>
> 2.2.1 Prevalence of stunting (height for age <-2 standard deviation from the median of the World Health Organization (WHO) Child Growth Standards) among children under 5 years of age
>
> 2.2.2 Prevalence of malnutrition (weight for height >+2 or <-2 standard deviation from the median of the WHO Child Growth Standards) among children under 5 years of age, by type (wasting and overweight)
>
> 2.2.3 Prevalence of anaemia in women aged 15 to 49 years, by pregnancy status (percentage)

This target is interpreted to cover research about reducing malnutrition and improving the nutritional status for all people (although children, girls, the elderly and pregnant women are mentioned specifically, the target does not seem limited to them). Malnutrition includes both underweight and overweight (<a id="WHOmalnut">[WHO, 2021](#f4)</a>); this factsheet was used to add terms, including specific micronutrients of worldwide importance (iodine, iron, vitamin A).

This query consists of 3 phrases. Phrase 1 focuses on negative actions, phrase 2 on positive actions. Phrase 3 is for terms which need to be combined with human terms.

#### Phrase 1

The general structure is *malnutrition + action*

`dietary NEAR/3 deficiency` finds a number of specific ones (e.g. dietary selenium deficieny, dietary Zn deficiency). `minerals` is not used - it only adds a few results, and many are from agriculture. `obese` is not included alone, as it tends to be used as a descriptor for a subject group, e.g. "reducing condition x in obese adults", rather than reducing obesity itself. `undernutrition` and other terms are included in phrase 3.

```Ceylon =
TS=
(
  (
      ("malnutrition" OR "malnourish*"
      OR "kwashiorkor" OR "marasmus"
      OR "anaemia" OR "anemia"
      OR
        (
          ("deficien*"OR "inadequa*")
          NEAR/3
              ("vitamin$" OR "micronutrient$" OR "iron" OR "iodine"
              OR "nutritional" OR "dietary"
              )
        )
      OR
        (
          ("stunting" OR "stunted" OR "wasting" OR "underweight")
          NEAR/15
              ("child*" OR "infant$" OR "under five$" OR "babies")
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

The general structure is *nutritional access/quality/status + action*

`stability` is not used in combination with food/nutrition as there are results about nutritional stability in processed foods. `nutritio*` should cover terms such as "access to nutritional care".

``` Ceylon =
TS=
(
  (
    (
      ("nutritio*")
      NEAR/5
        ("access" OR "safe" OR "unsafe"
        OR "secure" OR "insecurity" OR "reliable" OR "reliability"    
        )
    )
  OR "diet* quality" OR "nutrition* security" OR "nutrition* quality" OR "nutrition sensitive agriculture"
  OR
    (
      ("nutritio*" OR "folate status" OR "micronutrient$")
      NEAR/5
          ("women" OR "girls" OR "mother$" OR "pregnancy"
          OR "child*" OR "infant$" OR "under five$" OR "babies" OR "perinatal"
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

The general structure is *undernutrition/food supply + actions + humans*. For the topics `"protein deficiency"  OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition"` and `food supply` there was a considerable number of papers from e.g. animals and therefore they had to be combined with "human" terms

``` Ceylon =
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
    OR "children" OR "child" OR "under fives" OR "infant$" OR "babies" OR "adolescent$" OR "adult$"
    OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys"
    OR "agricultur*" OR "food security" OR "poverty"
    OR "rural" OR "urban" OR "countr*" OR "nation$" OR "develop* state$" OR "agricultur*"
    )
)

```

## Target 2.3

> **2.3 By 2030, double the agricultural productivity and incomes of small-scale food producers, in particular women, indigenous peoples, family farmers, pastoralists and fishers, including through secure and equal access to land, other productive resources and inputs, knowledge, financial services, markets and opportunities for value addition and non-farm employment.**
>
> 2.3.1 Volume of production per labour unit by classes of farming/pastoral/forestry enterprise size
>
> 2.3.2 Average income of small-scale food producers, by sex and indigenous status

This target is interpreted to include research about increasing the productivity and income of small-scale food producers (terrestrial and aquatic). Specific ways to do this are mentioned (securing access, rights, and opportunities for non-farm employment/value addition), so these are included too.

This query consists of 1 phrase. The basic structure is *action + productivity/access etc. + small-scale food producers*

 For the *small-scale food prodcer terms*, `small scale`+ `farm*` will cover types of farming in two words e.g. forest farming. The phrase may seem complex, but adding the specific types of crops with `production` etc. adds around 300 results over the last 5 years. Types of farming system were expanded using MeSH (NIH) and Emtree (Embase database, Elsevier) subject vocabularies. Specific types of crops and livestock were further expanded using FAO statistical year book (<a id="FAO2013">[FAO, 2013](#f2)</a>). For crops, those listed as major crops or "important food crops" are included, while oil crops were excluded (not being food). Some specific types are covered by generic terms: e.g. Root crops are covered by `crops`, and terms such as `farm*` will cover types of farming in two words e.g. forest farms, family farms, fish farming.

 In the *productivity/access etc. terms*:
 - `intensification` implies increasing production, but results in some noise when used alone - it can be used in other contexts, and finds many results about the *effects* of agricultural intensification, thus it is combined with other terms which limit it better to works looking at the process itself.
- Originally `"access*" OR "barrier$"` was combined with many other terms (access to...) - however I am not sure this is necessary, as the target is so broad in what should be accessible. A few irrelevant results are included due to the abstract including an "open access" publishing statement; and a couple from open access to e.g. satellite data. This is hard to exclude as we want "open access fisheries", for example. (Original combination with: `"farmland$" OR "land" OR "resources" OR "financial service$" OR "banking" OR "microfinance" OR "credit" OR "microcredit" OR "insurance" OR "microinsurance" OR "market$" OR "marketing" OR "traders" OR "trade" OR "agricultur* input$" OR "farm input$" OR "water" OR "machinery" OR "equipment" OR "technology" OR "farm* experience" OR "information" OR "training" OR "equitab*" OR "inequitab*"`)

``` Ceylon =
  TS= (
          (
            ("intensification" NEAR/5 ("smallhold*" OR "sustainable" OR "agroecolog*" OR "ecolog*"))  
          OR
            (
              ("production" OR "productivity" OR "yield$" OR "agricultural output$" OR "farm output$"
              OR "livelihood$" OR "income$" OR "profit*" OR "revenue" OR "economic viability"
              OR "value addition" OR "diversification" OR "non-farm employment" OR "off-farm employment" OR "off farm income"
              OR "access*" OR "empowerment" OR "benefit$"
              OR ("right$" NEAR/5 ("farmland$" OR "land" OR "property" OR "tenure"))
              OR ("distribution*" NEAR/5 ("equity" OR "equitable" OR "justice" OR "injustice"))
              )
              NEAR/5
                ("improve*" OR "increase*" OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
                OR "more efficie*" OR "better" OR "raise" OR "bolster" OR "strengthen*" OR "empower" OR "empowering"
                OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
                )
            )
          OR
            (
              ("barrier$" OR "obstacle$"
              OR ("distribution*" NEAR/5 "injustice")
              OR "land grab*"
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

## Target 2.4

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

``` Ceylon =
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
              ("production" OR "productivity" OR "yield$" OR "agricultural output$" OR "farm output$")
              NEAR/5
                ("improve*" OR "increase*" OR "enhanc*" OR "stimulat*"
                OR "more efficie*" OR "better" OR "raise" OR "bolster" OR "strengthen*"
                )
            )
          )  
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*")
)
```  

#### Phrase 2

Phrase 2 and 3 concern reducing vulnerability / increasing resilience. They have the same terms for food production systems, but differ in the terms for resilience: phrase 2 is linked to general terms for resilience, while phrase 3 covers terms need to be connected to disasters/shocks/risks.

Resilience in terms of food production has been described by FAO as:
> " In the context of sustainable food and agriculture, resilience is the capacity of agro-ecosystems, farming communities, households or individuals to maintain or enhance system productivity by preventing, mitigating or coping with risks, adapting to change, and recovering from shocks" (<a id="FAO2014">[FAO, 2014, p.28](#f7)</a>)

The basic structure of phrase 2 is *food production systems + resilience/vulnerability + action*.

In the *food production system* terms, production systems and species are included (i.e. species are split from production where possible so that both resilience for the species and the production system will be covered). Some species remain linked to production to avoid irrelevant results (e.g. vegetable intake and psychological resilience). `pastoral*` is limited in this phrase, as it finds results from other uses (pastoral care, religion studies).

In the *resilience* terms, `tolera*` is a particularly influential term that increases results ("drought tolerance" of crops being a common research theme). `climate smart agriculture` is a term used for an approach specifically addressing climate change.

``` Ceylon =
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
                  OR "improve*" OR "increase" OR "increasing" OR "maintain*"
                  OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "strengthen*" OR "empower" OR "empowering"
                  OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
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

The basic structure of phrase 3 is *food production systems + disaster/climate change + action*.

The *food production system* terms are the same as phrase 2.  These *disaster/climate change* terms include natural disasters, climate, market volatility, civil and political unrest (examples of risks in <a id="FAO2014">[FAO, 2014](#f7)</a>).

``` Ceylon =
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
                    OR "improve*" OR "increase" OR "increasing" OR "maintain*"
                    OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "strengthen*"
                    )
                )
              )
              NEAR/5
                      ("climate change" OR "climatic change$" OR "global warming" OR "changing climate"
                      OR "disaster$" OR "catastroph*"
                      OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$"))
                      OR "drought$" OR "flood*" OR "heatwave$" OR "heat-wave$" OR "cold spells"
                      OR "wildfire*" OR "forest fire*" OR "wild-fire*" OR "forestfire*"
                      OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "storm$"
                      OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$"
                      OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "surface collapse$" OR "mud flow$" OR "mud-flow$"
                      OR "tipping point$"  
                      OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) OR "tsunami*"
                      OR (("volatil*" OR "unstable" OR "instability") NEAR/5 ("market$" OR "price$"))
                      OR "financial crash*" OR "economic downturn$"
                      OR "war" OR "wars"
                      OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
                      OR "outbreak$" OR "disease risk$" OR "pandemic$" OR "epidemic$"
                      )
          )
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*" OR "wild pig$")
)
```

#### Phrase 4

The general structure is *ecoagriculture + action // food production systems + sustainability + action*.

`ecoagricultur*` is a relatively specialist term for ecology and agriculture and considered narrow enough to use alone.

Other terms suggesting research about sustainable agriculture were combined with the agricultural terms. `agroecolog*` (agroecology, or the agroecological approach) is considered a relevant term for sustainable, being related to ecology and environmental stability as well as social and cultural dimensions (<a id="SFS">[One Planet network Sustainable Food Systems (SFS) Programme, 2020, p. 28](#f8)</a>). Other terms for practices/approaches that can be considered to contribute to "sustainable food production systems" were gathered from <a id="HLPE">[High Level Panel of Experts on Food Security and Nutrition (2019, Appendix 1 and p. 36)](#f14)</a>; some of these also are relevant for soil quality. Other terms from this source are included in other phrases: "sustainable intensification" is covered in phrase 1, "climate smart agriculture" in phrase 2. `organic` must be combined due to use in other contexts (e.g. soil organic matter, organic carbon).

``` Ceylon =
TS=
  (
    ("ecoagricultur*" OR "eco-agricultur*" OR "permaculture"
    OR "conservation agriculture" OR "conservation farming"
    )
    NEAR/5
        ("adopt*" OR "apply" OR "implement*" OR "establish*" OR "build*"
        OR "improve*" OR "increase" OR "increasing" OR "maintain*"
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
          ("sustainab*" OR "agroecolog*"
          OR ("organic" NEAR/3 ("farm*" OR "agricultur*" OR "cultivation" OR "gardening" OR "production" OR "orchard$" OR "pasture$" OR "aquaculture"))
          OR "eco-friendly" OR "ecosystem approach"
          OR "natural pest control" OR "natural pest management" OR "biological pest control"
          OR "intercropping" OR "cover crop$" OR "crop rotation" OR "polyculture$"
          OR "reduced tillage" OR "mulch" OR "mulching"
          OR "water conservation"       
          )
          NEAR/5
              ("adopt*" OR "apply" OR "implement*" OR "establish*" OR "build*"
              OR "improve*" OR "increase" OR "increasing" OR "maintain*"
              OR "enhanc*" OR "promot*" OR "stimulat*" OR "encourag*" OR "strengthen*" OR "empower" OR "empowering"
              OR  "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
              )
        )   
    )
    NOT ("solar farm*" OR "wind farm*" OR "power farm*")  
)
```

#### Phrase 5

The general structure is *food production systems + ecosystems and soil + action*. - this phrase covers "positives", phrase 6 covers "negatives". Some terms are already covered in phrase 4 (e.g. reduced tillage)

``` Ceylon =
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

The general structure is *food production systems + ecosystems and soil + action*. - this phrase covers "negatives", phrase 5 covers "positives".

Types of land/soil degradation are taken from <a id="FAO2014">[FAO (2014)](#f7)</a> and (<a id="SDGindmetadata">[Statistics Division, 2021b (Indicator 2.4.1)](#f9)</a>).

``` Ceylon =
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

## Target 2.5

> **2.5 By 2020, maintain the genetic diversity of seeds, cultivated plants and farmed and domesticated animals and their related wild species, including through soundly managed and diversified seed and plant banks at the national, regional and international levels, and promote access to and fair and equitable sharing of benefits arising from the utilization of genetic resources and associated traditional knowledge, as internationally agreed.**
>
> 2.5.1 Number of (a) plant and (b) animal genetic resources for food and agriculture secured in either medium- or long-term conservation facilities
>
> 2.5.2 Proportion of local breeds classified as being at risk of extinction

This target is interpreted to cover research about:
* The preservation of diversity of farmed species/wild relatives (phrases 1,2).
* Agricultural genetic banks and preservation of tissue (seed, plant, animal) (phrase 3).
* Benefit sharing for genetic resources and traditional knowledge related to food and agriculture (phrases 4,5).

The FAO Second Global Assessment of Animal Genetic Resources was used as a source of terms (<a id="FAO2015">[Commission on Genetic Resources for Food and Agriculture Assessments, 2015](#f11)</a>). Central instruments are The Treaty on Plant Genetic Resources for Food and Agriculture, the Convention on Biological Diversity and elaborations in the Nagoya Protocol.

Types of farming system were expanded using MeSH (NIH) and Emtree (Embase database, Elsevier) subject vocabularies. Specific types of crops and livestock were further expanded using FAO statistical year book (<a id="FAO2013">[FAO, 2013](#f2)</a>). For crops, those listed as major crops or "important food crops" are included, while oil crops were excluded (not being food). Some specific types are covered by generic terms: e.g. Root crops are covered by `crops`, and terms such as `farm*` will cover types of farming in two words e.g. forest farms, family farms, fish farming.

This query consists of 5 phrases.

#### Phrase 1

The general structure is *agricultural diversity/landraces + action* - this phrase covers terms which are used in the context of agricultural diversity. Phrase 2 expands.

Conserving wild relatives and traditional varieties is considered maintaining genetic diversity. `agrobiodiversity` is wider than only the species used in agriculture - it covers also the non-harvested species that support production and agro-ecosystems (e.g. pollinators, soil-organisms) (<a id="FAO2004">[FAO, 2004](#f10)</a>). It is considered relevant and included, as although the target does not focus on these supporting species, research about agrobiodiversity is likely looking at the whole system (i.e. supporting diversity AND agricultural diversity). `conserv*` will cover e.g. conservation breeding, on-farm conservation etc..

``` Ceylon =
TS=
(
    ("agricultural diversity" OR "agricultural biodiversity" OR "agrobiodiversity"
    OR "landrace$" OR "wild relative$"
    OR  
      (
        ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
        NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
      )
    OR "plant genetic resource$" OR "animal genetic resource$"
    )
    NEAR/5
        ("maintain*" OR "conserv*" OR "preserv*" OR "protect*"
        OR "Convention on biological diversity"
        OR
          (
            ("loss" OR "extinction")
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

``` Ceylon =
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
                        ("loss" OR "extinction")
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

The general structure is *gene banks + action + agriculture*

The action terms for genebanks helps to filter out results which mention genebanks that were used in research (i.e. samples were taken from...).

`cryoconservation` and `cryopreservation` are ex situ in vitro methods of conservation of diversity (<a id="FAO2015">[Commission on Genetic Resources for Food and Agriculture Assessments, 2015](#f11)</a>); research about cryopreservation for relevant groups is thus considered relevant.

`domestic*` was removed from the agriculture terms as results were mostly about domestic cats.

``` Ceylon =
TS=
(
  (
      ("cryoconservation"
      OR
        (
          ("plant bank$" OR "seed bank$" OR "gene bank$" OR "genebank$" OR "germplasm bank$" OR "cryobank$"
          )
          NEAR/15
              ("diversity" OR "genetic resources" OR "agricultural biodiversity"
              OR "maintain*" OR "conserv*" OR "preserv*" OR "protect*" OR "extinct*" OR "endangered"
              OR "establish*" OR "support" OR "build*" OR "strengthen*"
              OR "collection$ management" OR "collection$ development"
              OR "funding" OR "policy" OR "policies"
              )
        )
      OR
        ("cryopreservation"
        NEAR/15
            ("diversity" OR "genetic resources" OR "agricultural biodiversity"
            OR "conserv*" OR "extinct*" OR "endangered"
            OR "germplasm" OR "oocyte$" OR "sperm*" OR "semen" OR "embryo$" OR "somatic cells"
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

Within the CBD/Nagoya protocol, benefits can be monetary/non-monetary (e.g. research results, royalties), related to using/commercialisation of genetic resources. "Using" includes research on genetics/biochemistry, development and biotechnology. (<a id="Garforth">[Garforth, 2018, p.3](#f12)</a>). However, the string is set up so that we do not need to define benefits or use types. The general structure is *genetic resources/knowledge + sharing/access + agriculture/food*

`access OR accessing OR accessib*` is used here to prevent "accessions". `biopiracy` is the unfair exploitation of biological resources/traditional knowledge. `traditional NEAR knowledge` etc. will cover e.g. traditional agricultural knowledge.

``` Ceylon =
TS=
(
    ("genetic resource$"
    OR "germplasm" OR "plant bank$" OR "seed bank$" OR "gene bank$" OR "genebank$" OR "germplasm bank$" OR "cryobank$"
    OR "seed commons"
    OR "bioprospecting"
    OR (("traditional" OR "indigenous" OR "autochthonous") NEAR/3 ("knowledge"))
    )
    NEAR/15
        ("sharing" OR "equitab*" OR "inequitable" OR "fair"
        OR "ownership" OR "access" OR "accessing" OR "accessib*" OR "right$"
        OR "governance"
        OR "material transfer agreement$" OR "informed consent"
        OR "Nagoya Protocol"
        OR "International Seed Treaty"
        OR "biopiracy"
        )
    NEAR/15
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
)   
```

#### Phrase 5

Phrase 5 is similar to phrase 4, with a focus on research that mentions instruments/treaties related to benefit sharing/access of genetic resources and traditional knowledge. The general structure is *genetic resources + agriculture/food + instruments*

`traditional NEAR knowledge` etc. will cover e.g. traditional agricultural knowledge.

``` Ceylon =
TS =
(
    ("genetic resource$"
    OR "bioprospecting"
    OR (("traditional" OR "indigenous" OR "autochthonous") NEAR/3 ("knowledge"))
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
        OR "Plant Genetic Resources for Food and Agriculture"
        )
)

```


## Target 2.a

> **2.a Increase investment, including through enhanced international cooperation, in rural infrastructure, agricultural research and extension services, technology development and plant and livestock gene banks in order to enhance agricultural productive capacity in developing countries, in particular least developed countries.**
>
> 2.a.1 The agriculture orientation index for government expenditures
>
> 2.a.2 Total official flows (official development assistance plus other official flows) to the agriculture sector

This target is interpreted to cover research about investment and international collaboration in rural infrastructure, agricultural research & technology, and gene banks. It is difficult to decide if this should be limited to research about developing countries - while target indicates that the results of these investments and collaborations should benefit LDCs, that does not necessarily mean that research on these themes is only beneficial if carried out in LDCs. An optional phrase for combining with LDCs is included below.

This query consists of 1 phrase

``` Ceylon =
TS =
    (
        "Agriculture Orientation Index for Government Expenditure$"
        OR
          (
            ("invest" OR "investing" OR "investment$"
            OR "government expenditure" OR "public spending"
            OR "development aid" OR "development assistance"
            OR "international cooperation" OR "international collaboration"
            )
            NEAR/15
                ("rural infrastructure"
                OR "agronom*" OR "agroecolog*" OR "agro ecolog*" OR "agricultural sector"
                OR "plant bank$" OR "seed bank$" OR "gene bank$" OR "genebank$" OR "germplasm bank$" OR "cryobank$"
                OR
                  (
                      ("infrastructure" OR "technolog*" OR "biotech*" OR "research" OR "science$" OR "innovation"
                      )
                      NEAR/3 ("agricultur*" OR "farm*" OR "irrigation" OR "agri food")
                  )                  
                )
          )
    )

```

Optional LDC phrase, can be combined with `AND`

```Ceylon =
TS=         ("developing world"
            OR
              (
                  ( "developing" OR "least developed" )
                  NEAR/3 ("state$" OR "nation$" OR "countr*")
              )
            OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
            OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "St Lucia" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa" OR "Sao Tome" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "Tuvalu" OR "Vanuatu" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
            OR "Afghanistan" OR "Armenia" OR "Azerbaijan" OR "Bhutan" OR "Bolivia" OR "Botswana" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "Ethiopia" OR "Kazakhstan" OR "Kyrgyzstan" OR "Kyrgyz Republic" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "Mali" OR "Mongolia" OR "Nepal" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova" OR "Rwanda" OR "South Sudan" OR "Swaziland" OR "Tajikistan" OR "Turkmenistan" OR "Uganda" OR "Uzbekistan" OR "Zambia" OR "Zimbabwe"        
            )


```

## Target 2.b

> **2.b Correct and prevent trade restrictions and distortions in world agricultural markets, including through the parallel elimination of all forms of agricultural export subsidies and all export measures with equivalent effect, in accordance with the mandate of the Doha Development Round.**
>
> 2.b.1 Agricultural export subsidies

This target is interpreted to cover research about export subsidies (and equivalents) for agricultural/food exports, and trade restrictions and distortions for world agricultural/food markets. A WTO agricultural export subsidy fact sheet (<a id="WTOexport">[Information and External Relations Division of the WTO Secretariat, n.d.](#f13)</a>) was used as a source of terms, where food aid is also a factor. There are not many works about this topic found.

This query consists of 2 phrases

#### Phrase 1:

``` Ceylon =
TS=
(
  ("export subsid*" OR "export credit$" OR "export financ*" OR "export competition" OR "export support$")
  AND
      ("agricultur*" OR "food")
)
```

#### Phrase 2:

```Ceylon =
TS=
(
  ("distort*" OR "price-fixing"
  OR "trade restrict*" OR "Doha" OR "food aid"
  OR "state support*" OR "state financial support"
  )
  NEAR/15
      (
        ("trade" OR "trading" OR "market$" OR "export$")
        NEAR/5 ("agricultur*" OR "food")
      )
)
```

## Target 2.c

> **2.c Adopt measures to ensure the proper functioning of food commodity markets and their derivatives and facilitate timely access to market information, including on food reserves, in order to help limit extreme food price volatility.**
>
> 2.c.1 Indicator of food price anomalies

This target is interpreted to cover research about preventing price volatility in food/agriculture. It consists of two phrases, where the basic structure is *action + prices + volatility + agriculture*.

#### Phrase 1:

```Ceylon =
TS=
(
  (
    ("prevent*" OR "avoid" OR "limit" OR "reduc*" OR "minimi*"
    OR "mitigat*" OR "tackl*" OR "combat" OR "counteract"
    OR "stabiliz*" OR "stabilis*"
    OR "policy" OR "policies"
    )
    NEAR/5
        ("price$" OR "market$")
    NEAR/5
        ("volatil*" OR "instability" OR "unstable" OR "anomalies")
  )
  AND ("food" OR "agricultur*")
)
```

```Ceylon =
TS=
(
  (
    (
      ("stabili*" OR "well functioning")
      NEAR/5
         ("price$" OR "market$")
    )
  OR
    (
      ("ensur*" OR "increas*" OR "improv*" OR "encourag*" OR "maintain*" OR "strengthen*"
      OR "policy" OR "policies" OR "intervention$"
      )
      NEAR/5
          ("price$" OR "market$")
      NEAR/5
          ("stable" OR "functioning")
    )
  )  
  AND ("food" OR "agricultur*")
)
```


## SDG generic

```Ceylon =
TS=
(
  "SDG2" OR "SDG$ 2" OR "SDG-2" OR "sustainable development goal$ 2"
  OR
    (
      ( "sustainable development goal$" OR "SDG$" OR "goal 2" )
      NEAR/15 ( "hunger" )
    )
)
```

## 4. Authorship and review

## 5. Footnotes

<a id="f5"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f11"></a> Commission on Genetic Resources for Food and Agriculture Assessments. (2015). *The Second Report on the State of the World’s Animal Genetic Resources for Food and Agriculture*. FAO. https://www.fao.org/publications/sowangr/en/

<a id="f10"></a> FAO. (2004). *What is Agrobiodiversity?* in "Building on Gender, Agrobiodiversity and Local Knowledge" [Training manual]. https://www.fao.org/3/y5609e/y5609e.pdf [↩](#FAO2004)

<a id="f2"></a> FAO statistical year book. (2013). *Part 3 Feeding the world*. ISBN: 9789251073964. http://www.fao.org/publications/card/en/c/1d6e6a08-4937-5c7d-8665-3e0ed6f29244

<a id="f7"></a> FAO. (2014). *Building a Common Vision for Sustainable Food and Agriculture. Principles and Approaches*. https://www.fao.org/3/a-i3940e.pdf [↩](#FAO2014)

<a id="f12"></a> Garforth, C. (2018). "An Introduction to the Nagoya Protocol on Access to Genetic Resources and the Fair and Equitable Sharing of Benefits Arising from their Utilization" in *Proceedings of the International Workshop on Access and Benefit-sharing for Genetic Resources for Food and Agriculture*. FAO. https://www.fao.org/3/CA0099EN/ca0099en.pdf [↩](#Garforth)

<a id="f14"></a> High Level Panel of Experts on Food Security and Nutrition. (2019). *Agroecological and other innovative approaches for sustainable agriculture and food systems that enhance food security and nutrition*. A report by the High Level Panel of Experts on Food Security and Nutrition
of the UN Committee on World Food Security, Rome. https://www.fao.org/cfs/cfs-hlpe [accessed 03 Jan 2022] [↩](#HLPE)

<a id="f8"></a> One Planet network Sustainable Food Systems (SFS) Programme. (2020). *Towards a Common Understanding of Sustainable Food Systems. Key approaches, concepts, and terms*. https://www.oneplanetnetwork.org/knowledge-centre/resources/towards-common-understanding-sustainable-food-systems-key-approaches [↩](#SFS)

<a id="f6"></a> Rivest, Maxime; Kashnitsky, Yury; Bédard-Vallée, Alexandre; Campbell, David; Khayat, Paul; Labrosse, Isabelle; Pinheiro, Henrique; Provençal, Simon; Roberge, Guillaume; James, Chris. (2021). *Improving the Scopus and Aurora queries to identify research that supports the United Nations Sustainable Development Goals (SDGs) 2021* V3. [Dataset]. doi: 10.17632/9sxdykm8s4.3 [↩](#Els)

<a id="f1"></a> Statistics Division. (2021a). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f9"></a> Statistics Division. (2021b). *SDG Indicators Metadata Repository*. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/metadata/ [accessed 8 December 2021] [↩](#SDGindmetadata)

<a id="f3"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/ [↩](#UNLDCs)

<a id="f4"></a> WHO. (2021, June 9). *Malnutrition*. [Fact sheet]. https://www.who.int/news-room/fact-sheets/detail/malnutrition. [↩](#WHOmalnut)

<a id="f13"></a> Information and External Relations Division of the WTO Secretariat. (n.d.). *Export subsidies and other export support measures* [Fact sheet]. World Trade Organization. https://www.wto.org/english/tratop_e/agric_e/factsheetagric17_e.htm [accessed 31 Dec 2021] [↩](#WTOexport)
