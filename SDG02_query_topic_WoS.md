# Search query for SDG 2 - Zero Hunger, Bergen topic-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 2
3. Documentation and string sections for each target

## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG2</summary>

```
TS=( ( ("malnutrition" OR "malnourish*" OR "end hunger" OR "ending hunger" OR "ends hunger" OR "world hunger" OR "famine$" OR "food insecurity" OR "unsafe food" OR "kwashiorkor" OR "marasmus" OR (("stunting" OR "wasting" OR "obesity" OR "overweight") NEAR/10 ("child*" OR "infant$")) ) ) OR ( ( "food supply chain$" OR "food security" OR "food safety" OR (("nutritional needs" OR "nutritional status") NEAR/15 ("women" OR "girls" OR "child*" OR "old* person$" OR "old* people" OR "elderly") ) ) ) OR ( ( (("protein deficiency" OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition") ) OR ( "food supply" ) ) AND ("humans" OR "humanity" OR "human" OR "people" OR "person$" OR "children" OR "child" OR "infant$" OR "babies" OR "adult$" OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys" OR "patient$" OR "rural" OR "urban" OR "countr*" OR "nation$" OR "develop* state$" OR "agricultur*" ) ) OR ( ( "productivity" OR "yield$" OR "production" OR "income$" OR "value addition" OR "non-farm employment" OR "property rights" OR "land grab*" OR ("access" NEAR/5 ("farmland$" OR "land" OR "financial service$" OR "market$" OR "agricultur* input$" OR "farm input$")) ) AND ( "smallhold*" OR "family farm*" OR (("small-scale" OR "indigenous" OR "homestead*") NEAR/5 ("food producer$" OR "farm*" OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoralist$" OR "agroforest*" OR "aquaculture" OR "fisher*" OR (("food" OR "agricultur*" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks") NEAR/5 ("production" OR "producer$") ) ) ) ) ) OR ( ( "food production" OR "food supply" OR "food supplies" OR "agricultur*" OR "ecoagricultur*" OR "eco-agricultur*" OR "farm*" OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoralist$" OR "agroforest*" OR "aquaculture" OR "fisher*" OR (("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks") NEAR/5 ("production" OR "producer$") ) ) AND ( "sustainab*" OR "eco-friendly" OR "resilient agricultur*" OR (("adapt*" OR "resilien*" OR "mitigat*" OR "vulnerab*" OR "cope" OR "coping" OR "preparedness" OR "early warning" OR "protect*") NEAR/10 ("disaster$" OR "drought$" OR "flood*" OR "climate change" OR "climatic change$" OR "global warming" OR "changing climate" OR ("extreme$" NEAR/2 ("climat*" OR "weather" OR "precipitation")) ) ) OR (("soil quality" OR "land quality" OR "biodiversity" OR "ecosystem function*") ) ) ) OR ( ( (("genetic diversity" OR "genetic resource$") ) OR "plant bank$" OR "seed bank$" OR "gene bank$" OR "germplasm bank$" ) NEAR/15 ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock" OR "poultry" OR "cattle" OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$" OR (("seed$" OR "plant$" OR "animal$" OR "breed$" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks") NEAR/5 ("domestic*" OR "farm*" OR "agricultur*" OR "cultiva*" OR "wild variet*" OR "wild relative$")) ) ) OR ( ("agricultural diversity" OR "agricultural biodiversity" OR "agrobiodiversity") ) OR ( (("genetic resource$" OR "germplasm" OR "bioprospecting" OR "traditional knowledge") NEAR/15 ("agricultur*" OR "farming" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks" OR "cultiva*" OR "wild variet*" OR "wild relativ*" OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$") ) ) OR ( ("genetic resource$" OR "germplasm" OR "bioprospecting" OR "traditional knowledge") AND ("agricultur*" OR "farming" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks" OR "cultiva*" OR "wild variet*" OR "wild relativ*" OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$") AND ("convention on biological diversity" OR "CBD" OR "Plant Genetic Resources for Food and Agriculture" OR "PGRFA" OR "Nagoya Protocol" OR "International Seed Treaty" OR "biopiracy") ) OR ( ( "Agriculture Orientation Index for Government Expenditure$" OR (("invest" OR "investing" OR "investment$" OR "international cooperation" OR "official development aid" OR "official development assistance") AND ("rural infrastructure" OR "food security" OR "food insecurity"OR "agronomy" OR "agroecology" OR (("sustainab*" OR "infrastructure" OR "technolog*" OR "research" OR "science$") NEAR/3 "agricultur*") ) ) ) AND ( (("developing" OR "least developed") NEAR/3 ("state$" OR "nation$" OR "countr*")) OR "developing world" OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands" OR "Afghanistan" OR "Armenia" OR "Azerbaijan" OR "Bhutan" OR "Bolivia" OR "Botswana" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "Ethiopia" OR "Kazakhstan" OR "Kyrgystan" OR "Lao People’s Democratic Republic" OR "Lesotho" OR "Malawi" OR "Mali" OR "Mongolia" OR "Nepal" OR "Niger" OR "Paraguay" OR "Republic of Moldova" OR "Rwanda" OR "South Sudan" OR "Tajikistan" OR "The former Yugoslav Republic of Macedonia" OR "Turkmenistan" OR "Uganda" OR "Uzbekistan" OR "Zambia" OR "Zimbabwe" ) ) OR ( ("export subsid*" OR "export credit$") NEAR/5 ("agricultur*" OR "food") ) OR ( ("trade restrict*" OR "distort*" OR "price-fixing" OR "Doha") NEAR/5 (("trade" OR "market$") NEAR/5 ("agricultur*" OR "food")) ) OR ( (("food" OR "agricultur*") NEAR/3 ("price$")) NEAR/5 ("volatil*" OR "stabil*") ) OR ("SDG2" OR "SDG$ 2" OR "SDG-2" OR "sustainable development goal$ 2" OR (("sustainable development goal$" OR "SDG$" OR "goal 2") NEAR/15 ("hunger")) ) )
```

</details>

## 2. General notes

Source of Targets and Indicators:
Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021]
<sup id="SDGT+Is">[1](#f1)</sup>

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

This query consists of 3 phrases.

##### Phrase 1:
`Underfeeding` and `starvation` removed as seem to be used mostly in a medical/physiology context, rather than related to food security/ supply. Hunger qualified with `end` or `world` for the same reason.

```Ceylon =
TS=
(
   "malnutrition" OR "malnourish*"
    OR "end hunger" OR "ending hunger" OR "ends hunger" OR "world hunger" OR "famine$"
    OR "food insecurity" OR "unsafe food"
    OR "kwashiorkor" OR "marasmus"
    OR
    (
      ( "stunting" OR "wasting" OR "obesity" OR "overweight" )
      NEAR/10
          ("child*" OR "infant$")
    )
 )

```

##### Phrase 2:

``` Ceylon =
TS=
(
  "food supply chain$" OR "food security" OR "food safety"
  OR
  (
    ("nutritional needs" OR "nutritional status")
    NEAR/15
        ("women" OR "girls" OR "child*" OR "old* person$" OR "old* people" OR "elderly")
  )
)
```

##### Phrase 3:

For the topics `"protein deficiency"  OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition"` and `food supply`there was a considerable number of papers from e.g. animals and therefore they had to be combined with "human" terms

``` Ceylon =
TS=
(
  ("protein deficiency"  OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition"
    OR "food supply"  
  )
  AND
    ( "humans" OR "humanity" OR "human" OR "people" OR "person$"
      OR "children" OR "child" OR "infant$" OR "babies" OR "adult$"
      OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys" OR "patient$"
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

This query consists of 1 phrase.

Production and income of small-scale farmers is so specific that any publications mentioning these will likely be relevant to the target, thus no modifying words included.

Types of agricultural system expanded using MeSH and Emtree subject vocabularies.

Types of crops and livestock expanded using: FAO statistical year book (2013) <sup id="FAO2013">[1](#f1)</sup>. Major crops or "important food crops" included, oil crops excluded. Root crops covered by "crops" in phrase above.

Topic approach: `NEAR` changed to `AND`

``` Ceylon =
  TS= (
          ( "productivity" OR "yield$" OR "production"
            OR "income$" OR "value addition" OR "non-farm employment"
            OR "property rights" OR "land grab*"
            OR
            (
              ( "access" )
              NEAR/5
                ( "farmland$" OR "land" OR "financial service$" OR "market$" OR "agricultur* input$" OR "farm input$" )
            )
          )
          AND
             ( "smallhold*" OR "family farm*"
               OR
               (
                  ("small-scale" OR "indigenous" OR "homestead*" )
                  NEAR/5
                    (
                      ( "food producer$" OR "farm*" OR "cropping system$" OR "orchard$" OR "arable land$"
                        OR "pasture$" OR "pastoralist$" OR "agroforest*" OR "aquaculture" OR "fisher*"
                      )
                    OR
                      (
                         ( "food" OR "agricultur*"
                           OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
                           OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
                         )
                         NEAR/5
                            ( "production" OR "producer$" )
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

Topic approach: `NEAR` changed to `AND`

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
        AND
            ("sustainab*" OR "eco-friendly" OR "resilient agricultur*"
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
            OR "soil quality" OR "land quality" OR "biodiversity" OR "ecosystem function*"
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
      ("plant bank$" OR "seed bank$" OR "gene bank$" OR "germplasm bank$"
      OR "genetic diversity" OR "genetic resource$"
      )
      NEAR/15
          ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
          OR "livestock" OR "poultry" OR "cattle"
          OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$"
          OR
            (
              ("seed$" OR "plant$" OR "animal$" OR "breed$"
              OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
              )
              NEAR/5
                  ("domestic*" OR "farm*" OR "agricultur*" OR "cultiva*" OR "wild variet*" OR "wild relative$")
            )
          )
)
```

##### Phrase 2:

``` Ceylon =
TS=
(
  "agricultural diversity" OR "agricultural biodiversity" OR "agrobiodiversity"  
)
```

##### Phrase 3:

``` Ceylon =
TS=
(
  ("genetic resource$" OR "germplasm" OR "bioprospecting" OR "traditional knowledge")
  NEAR/15
      ("agricultur*" OR "farming"
      OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
      OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "ducks"
      OR "cultiva*" OR "wild variet*" OR "wild relativ*" OR "landrace$" OR "local breed$" OR "traditional variet*" OR "traditional breed$"
      )       
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
      ("Agriculture Orientation Index for Government Expenditure$"
      OR
        (
          ("invest" OR "investing" OR "investment$" OR "international cooperation"
          OR "official development aid" OR "official development assistance"
          )
          AND
              ("rural infrastructure" OR "food security" OR "food insecurity"OR "agronomy" OR "agroecology"
              OR
                (
                  ("sustainab*" OR "infrastructure" OR "technolog*" OR "research" OR "science$")
                  NEAR/3 "agricultur*"
                )                  
              )
        )
      )
      AND
          ("developing world"
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
      ("sustainable development goal$" OR "SDG$" OR "goal 2")
      NEAR/15 ("hunger")
    )
)
```

## Footnotes
<b id="f1">1</b> This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)".
(https://unstats.un.org/sdgs/indicators/indicators-list/) [↩](#SDGT+Is)

<b id="f2">2</b> FAO statistical year book (2013), Part 3 Feeding the world, ISBN: 9789251073964, http://www.fao.org/publications/card/en/c/1d6e6a08-4937-5c7d-8665-3e0ed6f29244.

<b id="f3">3</b> United Nations (2019) World Economic Situation and Prospects (Statistical Annex). https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)
