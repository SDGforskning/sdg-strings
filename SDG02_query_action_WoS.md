# Search query for SDG 2 - Zero Hunger, Bergen action-approach.

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

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Lists of least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) are from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) - countries were included if they appeared in the tables from 2016 to 2021 (i.e. were on these lists at any time between Nov 2015 and Dec 2020) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f3)</a>).

During editing of this string (2021), we have consulted two other sets of queries for reference: <a id="Aurora">[Aurora Universities network (2020)](#f5)</a> and <a id="Els">[Rivest et al. (2021)](#f6)</a>.

**Abbreviations**
* FAO - Food and Agriculture Organization of the United organizations
* WHO - World Health Organization
* MeSH - Medical Subject Headings - https://www.ncbi.nlm.nih.gov/mesh/

## 3. Targets

## Target 2.1/2.2

These targets are combined, as they cover similar topics.

> **2.1 By 2030, end hunger and ensure access by all people, in particular the poor and people in vulnerable situations, including infants, to safe, nutritious and sufficient food all year round.**
>
> 2.1.1 Prevalence of undernourishment
>
> 2.1.2 Prevalence of moderate or severe food insecurity in the population, based on the Food Insecurity Experience Scale (FIES)

> **2.2 By 2030, end all forms of malnutrition, including achieving, by 2025, the internationally agreed targets on stunting and wasting in children under 5 years of age, and address the nutritional needs of adolescent girls, pregnant and lactating women and older persons.**
>
> 2.2.1 Prevalence of stunting (height for age <-2 standard deviation from the median of the World Health Organization (WHO) Child Growth Standards) among children under 5 years of age
>
> 2.2.2 Prevalence of malnutrition (weight for height >+2 or <-2 standard deviation from the median of the WHO Child Growth Standards) among children under 5 years of age, by type (wasting and overweight)
>
> 2.2.3 Prevalence of anaemia in women aged 15 to 49 years, by pregnancy status (percentage)

These targets are interpreted to cover research about
* reducing hunger and all forms of malnurition for all people - although children are mentioned specifically, the target does not seem to limit to them.
* access to safe and nutritious food, reducing food insecurity, for all people

This query consists of 3 phrases. Phrase 1 focuses on negative actions, phrase 2 on positive actions. Phrase 3 is for terms which need to be combined with human terms.

Should `food/nutrition sovereignty` be included here, or does it go too far?

##### Phrase 1:

The general structure is *hunger/malnutrition + action*

Malnutrition includes both underweight and overweight (<a id="WHOmalnut">[WHO, 2021](#f4)</a>); this factsheet was used to add terms, including specific micronutrients of worldwide importance (iodine, iron, vitamin A). `dietary NEAR/3 deficiency` finds a number of specific ones not searched for (e.g. dietary selenium deficieny, dietary Zn deficiency). `minerals` is not used - it only adds a few results, and many are from agriculture. `Underfeeding` and `starvation` removed as seem to be used mostly in a medical/physiology context, rather than related to food security/supply. Hunger is used in phrases (`ending hunger`, `world hunger`) for the same reason. `feast and famine` refers to bioreactors/selective pressure in microbial cultures (not relevant). `undernutrition` and other terms are included in phrase 3.

```Ceylon =
TS=
(
  (
      ("end hunger" OR "ending hunger" OR "ends hunger" OR "world hunger" OR "hunger and poverty" OR "poverty and hunger"
      OR "famine$"
      OR "malnutrition" OR "malnourish*"
      OR "kwashiorkor" OR "marasmus"
      OR "inadequate vitamin$" OR "anaemia" OR "anemia"
      OR
        ("deficien*"
        NEAR/3
            ("vitamin$" OR "micronutrient$" OR "iron" OR "iodine"
            OR "nutritional" OR "dietary"
            )
        )
      OR
        (
          ("stunting" OR "stunted" OR "wasting")
          NEAR/15
              ("child*" OR "infant$")
        )
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
  NOT (("feast and famine" OR "feast-famine" OR "salmon anemia") NOT ("end* hunger" OR "malnutrition"))    
 )
```

`"obesity" OR "overweight"` can added to the above section (phrase 1) without issues - the action terms are identical - however, in terms of presenting results, separating out obesity may be useful for the user as it accounts for maybe 50 % of results.

```Ceylon =
TS=
(
  ("obesity" OR "overweight"
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
```

##### Phrase 2:

The general structure is *food security/safety/nutritional status + action*

`stability` is not used in combination with food/nutrition as there are results about nutritional stability in processed foods.

``` Ceylon =
TS=
(
  (
    (
      ("food" OR "nutrition*")
      NEAR/5
        ("access"
        OR "safe" OR "unsafe"
        OR "secure" OR "security" OR "insecurity" OR "reliable" OR "reliability"    
        )
    )
  OR "right to food"
  OR "food safety"
  OR
    (
      ("nutrition*" OR "folate status" OR "micronutrient$")
      NEAR/5
          ("women" OR "girls" OR "mother$" OR "pregnancy" OR "child*" OR "infant$" OR "perinatal"
          OR "old* persons" OR "old* people" OR "elderly")
    )
  )
  NEAR/5
     ("improv*" OR "enhanc*" OR "increas*" OR "strengthen" OR "attain" OR "achiev*"
     OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "manag*"
     OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
     )
)
```

##### Phrase 3:

The general structure is *undernutrition/food supply + actions + humans*

For the topics `"protein deficiency"  OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition"` and `food supply` there was a considerable number of papers from e.g. animals and therefore they had to be combined with "human" terms

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
    OR
    (
      ("food supply")
      NEAR/5
         ("improv*" OR "enhanc*" OR "increas*" OR "strengthen" OR "attain" OR "achiev*"
         OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "manag*"
         OR "legislat*" OR "policy" OR "policies" OR "strateg*" OR "framework$"
         )
    )  
  )
  AND
    ( "humans" OR "humanity" OR "human" OR "people" OR "person$"
      OR "children" OR "child" OR "infant$" OR "babies" OR "adolescent$" OR "adult$"
      OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys"
      OR "patient$" OR "poverty"
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

This query consists of 1 phrase. The basic structure is *productivity/access + small-scale food producers*

Types of agricultural system were expanded using MeSH (MEDLINE database, NIH) and Emtree (Embase database, Elsevier) subject vocabularies. Types of crops and livestock expanded using the FAO statistical year book (<a id="FAO2013">[FAO, 2013](#f1)</a>). Major crops or "important food crops" included, oil crops excluded. Root crops covered by `crops` in phrase above. `small scale`+ `farm*` will cover e.g. forest farming. The part for small-scale farming may seem complex, but adding the specific types of crops with `production` etc. adds around 300 results over the last 5 years.

``` Ceylon =
  TS= (
          (
            (
              ("production" OR "productivity" OR "yield$" OR "agricultural output$"
              OR "livelihood$" OR "income$" OR "profit*" OR "revenue" OR "economic viability"
              OR "benefit$"
              )
              NEAR/5
                ("improve*" OR "increase*" OR "enhance"
                OR "efficie*" OR "better" OR "raise" OR "bolster"
                )
            )
          OR "value addition" OR "non-farm employment" OR "off-farm employment"
          OR
            (
              ("access*" OR "barrier$")
              NEAR/5
                ("farmland$" OR "land"
                OR "financial service$" OR "banking" OR "microfinance" OR "credit" OR "microcredit" OR "insurance" OR "microinsurance"
                OR "market$" OR "marketing" OR "traders" OR "trade"
                OR "agricultur* input$" OR "farm input$" OR "agricultural resources" OR "water"
                OR "machinery" OR "equipment" OR "technology"
                OR "farm* experience" OR "information" OR "training"
                OR "equitab*" OR "inequitab*"
                )
            )
          OR "land grab*"
          OR "tenure"
          OR
            ("right$" NEAR/5 ("farmland$" OR "land" OR "property")
            )
          OR "distributional justice"  
          )
          AND
              ("smallhold*" OR "family farm*"
              OR
                (
                  ("small-scale" OR "indigenous" OR "homestead*")
                  NEAR/5
                    (
                      ("food producer$" OR "food production" OR "food grower$" OR "agricultur*"
                      OR "farm*" OR "cropping system$" OR "orchard$" OR "arable land$"
                      OR "pasture$" OR "pastoralist$" OR "agroforest*"
                      OR "aquaculture" OR "fisher*" OR "fish farm*"
                      )
                    OR
                      (
                        ("crop$" OR "produce" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
                        OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
                        )
                        NEAR/5
                            ("production" OR "producer$" OR "grower$")
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

This query consists of 1 phrase.

Types of agricultural system expanded using MeSH and Emtree subject vocabularies.

Types of crops and livestock expanded using: FAO statistical year book (2013) <sup id="FAO2013">[1](#f1)</sup>. Major crops or "important food crops" included, oil crops excluded. Root crops covered by "crops" in phrase above.

``` Ceylon =
TS= (
        ( "food production" OR "food supply" OR "food supplies"
          OR "agricultur*" OR "ecoagricultur*" OR "eco-agricultur*"
          OR "farm*" OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoralist$"
          OR "agroforest*" OR "aquaculture" OR "fisher*"
          OR
          (
            ( "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
              OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
            )
            NEAR/5
                ( "production" OR "producer$" )
          )      
        )
        NEAR/15
            ( "sustainab*" OR "eco-friendly" OR "resilient agricultur*"
              OR
              (
                ( "adapt*" OR "resilien*" OR "mitigat*" OR "vulnerab*" OR "cope" OR "coping"
                  OR "preparedness" OR "early warning" OR "protect*"
                )
                NEAR/10
                    ( "disaster$" OR "drought$" OR "flood*"
                      OR "climate change" OR "climatic change$" OR "global warming" OR "changing climate"
                      OR ("extreme$" NEAR/2 ("climat*" OR "weather" OR "precipitation"))
                    )
              )
              OR
              (
                ( "soil quality" OR "land quality" OR "biodiversity" OR "ecosystem function*" )
                NEAR/5
                  ( "improv*" OR "restor*" OR "enhanc*" OR "maintain*" OR "preserv*"
                    OR "conserv*" OR "protect*" OR "resilien*"
                  )
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

This query consists of 4 phrases.

Types of crops and livestock expanded using: FAO statistical year book (2013) <sup id="FAO2013">[1](#f1)</sup>. Major crops or "important food crops" included, oil crops excluded. Root crops covered by "crops" in phrase above.

##### Phrase 1:

Limitation of the topic (genetic resources) to agricultural resources by combining terms with agricultural terms (e.g. `poultry, livestock, cereals`).
Terms which can apply to wild species combined with agricultural concepts (e.g. `animal$`is combined with `"domestic* OR farm*"` etc.)

``` Ceylon =
TS=
(
    (
        ( "plant bank$" OR "seed bank$" OR "gene bank$" OR "germplasm bank$"
          OR
            (
                ( "genetic diversity" OR "genetic resource$" )
                NEAR/10
                ( "maintain*" OR "conserv*" OR "preserv*" OR "protect*" OR "extinct*" OR "endangered" )
            )
        )
        NEAR/15
            ( "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
              OR "livestock" OR "poultry" OR "cattle"
              OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$"
              OR
                (
                    ( "seed$" OR "plant$" OR "animal$" OR "breed$"
                       OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
                     )
                     NEAR/5
                         ( "domestic*" OR "farm*" OR "agricultur*" OR "cultiva*" OR "wild variet*" OR "wild relative$" )
                )
            )
    )
```

##### Phrase 2:

``` Ceylon =
TS=
(
    ( "agricultural diversity" OR "agricultural biodiversity" OR "agrobiodiversity" )
    NEAR/5
        ("maintain*" OR "conserv*" OR "preserv*" OR "protect*")        
)
```

##### Phrase 3:

``` Ceylon =
TS=
(
    (
        ( "genetic resource$" OR "germplasm" OR "bioprospecting" OR "traditional knowledge" )
        NEAR/15
            ( "agricultur*" OR "farming"
              OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
              OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
              OR "cultiva*" OR "wild variet*" OR "wild relativ*" OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$"
            )
    )
    NEAR/15
        ( "sharing" OR "equitab*" OR "fair" OR "ownership" OR "access*" )                
)   
```

##### Phrase 4:

`"convention on biological diversity" OR "CBD" OR "Plant Genetic Resources for Food and Agriculture" OR "PGRFA"OR "Nagoya Protocol" OR "International Seed Treaty"` Treaties/topics related to sharing/access/ownership of genetic resources and traditional knowledge

`biopiracy` - i.e. unfair exploitation of genetic resources/traditional knowledge

``` Ceylon =
TS =
(
    ( "genetic resource$" OR "germplasm" OR "bioprospecting" OR "traditional knowledge" )
    AND
        ( "agricultur*" OR "farming"
          OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
          OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
          OR "cultiva*" OR "wild variet*" OR "wild relativ*" OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$"
        )
    AND
        ( "convention on biological diversity" OR "CBD"
          OR "Plant Genetic Resources for Food and Agriculture" OR "PGRFA"
          OR "Nagoya Protocol"
          OR "International Seed Treaty"
          OR "biopiracy"
        )
)
```


## Target 2.A

> **2.a Increase investment, including through enhanced international cooperation, in rural infrastructure, agricultural research and extension services, technology development and plant and livestock gene banks in order to enhance agricultural productive capacity in developing countries, in particular least developed countries.**
>
> 2.a.1 The agriculture orientation index for government expenditures
>
> 2.a.2 Total official flows (official development assistance plus other official flows) to the agriculture sector

This query consists of 1 phrase

Genebanks already covered (Target 2.5), so not included as a term here.

Lists of least developed countries, small island developing states and landlocked developing states are from the United Nations World Economic Situation and Prospects (tables F, H and I, pages 173-174)<sup id="UNLDCs">[3](#f3)</sup>.

``` Ceylon =
TS =
    (
        ( "Agriculture Orientation Index for Government Expenditure$"
          OR
          (
              ( "invest" OR "investing" OR "investment$" OR "international cooperation"
               OR "official development aid" OR "official development assistance"
              )
              AND
                  ( "rural infrastructure" OR "food security" OR "food insecurity"OR "agronomy" OR "agroecology"
                    OR
                    (
                        ( "sustainab*" OR "infrastructure" OR "technolog*" OR "research" OR "science$" )
                        NEAR/3 "agricultur*"
                    )                  
                  )
          )
        )
        AND
            ( "developing world"
              OR
              (
                    ( "developing" OR "least developed" )
                    NEAR/3 ( "state$" OR "nation$" OR "countr*" )
              )
              OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
              OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands"
              OR "Afghanistan" OR "Armenia" OR "Azerbaijan" OR "Bhutan" OR "Bolivia" OR "Botswana" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "Ethiopia" OR "Kazakhstan" OR "Kyrgystan" OR "Lao People’s Democratic Republic" OR "Lesotho" OR "Malawi" OR "Mali" OR "Mongolia" OR "Nepal" OR "Niger" OR "Paraguay" OR "Republic of Moldova" OR "Rwanda" OR "South Sudan" OR "Tajikistan" OR "The former Yugoslav Republic of Macedonia" OR "Turkmenistan" OR "Uganda" OR "Uzbekistan" OR "Zambia" OR "Zimbabwe"            
            )
    )

```

## Target 2.B/2.C

> **2.b Correct and prevent trade restrictions and distortions in world agricultural markets, including through the parallel elimination of all forms of agricultural export subsidies and all export measures with equivalent effect, in accordance with the mandate of the Doha Development Round.**
>
> 2.b.1 Agricultural export subsidies

> **2.c Adopt measures to ensure the proper functioning of food commodity markets and their derivatives and facilitate timely access to market information, including on food reserves, in order to help limit extreme food price volatility.**
>
> 2.c.1 Indicator of food price anomalies

These targets were combined.

This query consists of 3 phrases

#### Phrase 1:

Although this appears to be a broad search, there are very few papers in this specialised  field. Therefore it was not limited further

``` Ceylon =
TS=
(
  ( "export subsid*" OR "export credit$" )
  NEAR/5
      ( "agricultur*" OR "food" )
)

```

#### Phrase 2:

```Ceylon =
TS=
(
  ( "trade restrict*" OR "distort*" OR "price-fixing" OR "Doha" )
  NEAR/5
      (("trade" OR "market$") NEAR/5 ("agricultur*" OR "food"))
)
```

#### Phrase 3:

```Ceylon =
TS=
(
  (
    ( "food" OR "agricultur*" )
    NEAR/3 ( "price$" )
  )
  NEAR/5
      ( "volatil*" OR "stabil*" )
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

<a id="f2"></a> FAO statistical year book. (2013). *Part 3 Feeding the world*. ISBN: 9789251073964. http://www.fao.org/publications/card/en/c/1d6e6a08-4937-5c7d-8665-3e0ed6f29244. [↩](#FAO2013)

<a id="f6"></a> Rivest, Maxime; Kashnitsky, Yury; Bédard-Vallée, Alexandre; Campbell, David; Khayat, Paul; Labrosse, Isabelle; Pinheiro, Henrique; Provençal, Simon; Roberge, Guillaume; James, Chris. (2021). *Improving the Scopus and Aurora queries to identify research that supports the United Nations Sustainable Development Goals (SDGs) 2021* V3. [Dataset]. doi: 10.17632/9sxdykm8s4.3 [↩](#Els)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f3"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f4"></a> WHO. (2021, June 9). *Malnutrition*. [Fact sheet]. https://www.who.int/news-room/fact-sheets/detail/malnutrition. [↩](#WHOmalnut)
