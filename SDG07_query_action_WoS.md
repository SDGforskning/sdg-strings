# Search query for SDG 7 - Affordable and clean energy, Bergen action-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 7
3. Documentation and string sections for each target

## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 7</summary>

Note that this query should be run in multiple steps, and then combined as shown in the final steps.

Search #1
```
TS= ( ( (("clean" OR "cleaner" OR "decarboni*" OR "low-carbon") NEAR/3 ( "fuel$" OR "energy" OR "power" OR "technolog*" OR "electricity" OR "cooking" OR "stove$" ) ) OR "solar cooker$" OR "solar box cooker$" ) NEAR/15 ("relian*" OR "primary use" OR "primary usage" OR "primary source$" OR "access*" OR "availab*" OR "barrier$" OR "obstacle$" OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$" OR "implement*" OR "adopt*" OR "transition$" OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation" OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning" OR "feed-in tariff$" OR "market$" OR "initiative$" OR (("energy" OR "green") NEAR/2 "certificat*") OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "sustainable development" OR "sustainable energy development" ) )
```
Search #2
```
TS=( ( ( "affordab*" OR "access*" OR "reliab*" OR "resilien*" OR "equitab*" OR (("develop*" OR "upgrad*" OR "invest" OR "investment$" OR "investing" OR "modern*") NEAR/10 "infrastructure") ) NEAR/15 ("electricity" OR "electrical grid" OR "electrical infrastucture" OR (("energy" OR "power") NEAR/2 ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply" OR "electrical" OR "infrastructure" OR "grid" OR "grids" OR "technolog*" OR "energy system$" OR "power system$") ) OR (("energy" OR "power" OR "electric" OR "electrical") NEAR/15 ("microgrid" OR "microgrids" OR "micro-grid" OR "micro-grids")) OR "off grid solution$" ) ) OR ( ("stable supply" OR "supply stability" OR "grid stability" OR ("moderni*" NEAR/3 ("energy" OR "power" OR "electricity" OR "grid" OR "grids")) OR "sustainable development" ) AND ("electricity" OR "electrical grid" OR "electrical infrastucture" OR (("energy" OR "power") NEAR/2 ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply" OR "electrical" OR "infrastructure" OR "grid" OR "grids" OR "technolog*" OR "energy system$" OR "power system$") ) OR ("microgrid" OR "microgrids" OR "micro-grid" OR "micro-grids") OR "off grid solution$" ) ) OR "universal electrification" OR "rural electrification" OR (("electrification" OR "electricity" OR "electrical supply" OR "energy service$" OR "energy access" OR "power supply") NEAR/15 ((("remote" OR "rural") NEAR/3 ("region$" OR "area" OR "areas" OR "communities" OR "community")) OR ("least developed" NEAR/3 ("countr*" OR "state$" OR "nation$")) OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" ) ) OR "energy security" OR "energy insecurity" OR "energy poverty" OR "energy vulnerability" OR "fuel poverty" OR "energy democracy" OR "energy justice" )
```

Search #3
```
TS=( "energy sector transformation" OR "renewable energy transition$" OR "national energy transition$" OR (("share" OR "shares" OR "proportion$" OR "percentage$") NEAR/3 ("renewables" OR "carbon-neutral" OR "green electricity" OR "green energy" OR "green power") ) OR ( ( "relian*" OR "primary use" OR "primary usage" OR "primary source$" OR "access*" OR "availab*" OR (("share" OR "shares" OR "proportion$" OR "percentage$") NEAR/2 ("generat*" OR "service$" OR "sector" OR "production" OR "supply" OR "energy system$" OR "power system$" OR "global energy" OR "global electricity" ) ) OR "barrier$" OR "obstacle$" OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$" OR "implement*" OR "adopt*" OR "energy transition$" OR "renewable transition$" OR "transition* to" OR "pathway to" OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation" OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning" OR "kyoto protocol" OR "feed-in tariff$" OR "market$" OR "initiative$" OR (("energy" OR "green") NEAR/2 "certificat*") OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "sustainable development" OR "sustainable energy development" ) NEAR/15 ( (("electricity" OR "power" OR "powered" OR "energy") NEAR/5 ( "renewable$" OR "sustainable" OR "hydrothermal" OR "geothermal" OR "hydroelectric" OR "hydropower" OR "hydrokinetic" OR "hybrid" OR "carbon-neutral" OR "green electricity" OR "green energy" OR "green power" ) ) OR "biofuel$" OR "bioenergy" OR "biodiesel" OR "solar cell$" OR "solar-cell$" OR "solar panel$" OR "solar-panel$" OR "solar power*" OR "solar array" OR "solar PV" OR "solar photovoltaic$" OR "solar thermal power" OR "solar thermal technolog*" OR "solar thermal collector$" OR "solar energy collector$" OR "solar district heating" OR "solar district cooling" OR "solar air heating system$" OR "solar space heating system$" OR ("solar thermal energy" NEAR/15 ("power" OR "electric*" OR "water heating" OR "industrial process heat*")) OR "wind farm$" OR "wind turbine$" OR "tidal turbine$" OR "stream turbine$" OR "current turbine$" OR (("biomass" OR "wind" OR "solar") NEAR/10 ("electric*" OR "generat*" OR "service$" OR "sector" OR "produc*" OR "supply" OR "technolog*" OR "energy system$" OR "power system$" OR "energy crop$" OR "energy security" OR "biofuel$" OR "bioenergy" OR "biodiesel" ) ) OR ("hydrogen" NEAR/10 ("renewable substitute$" OR "renewable source$")) OR (("fuel cell$" OR "battery" OR "batteries" OR "energy storage" OR "smart grid$") NEAR/15 ("renewable" OR "sustainab*")) ) ) )
```
Search #4
```
TS= ( ("energy intensity" AND ("energy consum*" OR "sustainab*" OR "energy efficiency" OR "GDP" OR "economic" OR "economy" OR "economies" OR "industry" OR "industrial" OR "manufacturing" OR ("emission$" NEAR/5 ("carbon" OR "co2")) OR "footprint$" OR "sustainable development" ) ) OR ( ("economic growth" OR "GDP") NEAR/15 ("energy use$" OR "energy consum*") ) )
```
Search #5
```
TS= ( (("increas*" OR "improv*" OR "double" OR "enhanc*" OR "better" OR "more efficient" OR "higher" OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning" OR "initiative$" OR (("energy" OR "green") NEAR/2 "certificat*") OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "energy sustainability" ) NEAR/15 ( "energy efficiency" OR "energy performance standard$" OR (("energy efficien*" OR "energy saving") NEAR/10 ("housing" OR "houses" OR "residential" OR "building$" OR "cities" OR "industry" OR "industrial" OR "manufacturing" OR "technolog*") ) ) ) OR ("energy efficiency" NEAR/15 "sustainable development") )
```
Search #6
```
TS= ( "caloric restriction" OR "calorie restriction" OR "metabolic syndrome" OR "muscle$" OR "mitochondria" OR "cardiovascular" OR "feed conversion" OR "animal energetics" OR "human energetics" OR ( ("metabolism" OR "metabolic") NOT ("climate change" OR "economy" OR "economies" OR "social metabolism" OR "urban metabolism" OR "urban energy" OR "economic metabolism" OR "socioeconomic metabolism" OR "societal metabolism" OR "industrial metabolism" OR "carbon metabolism" )) )
```
Search #7
```
TS= ( ( "technical knowledge transfer" OR "transfer of technical knowledge" OR "transfer of technolog*" OR "technology transfer$" OR (("research" OR "technology") NEAR/5 ("access*" OR "sharing" OR "shared benefit$")) OR "capacity building" OR "build capacity" OR "capacity development" OR "international cooperation" OR "international collaboration" OR "foreign aid" OR "official development aid" OR "official development assistance" ) NEAR/15 ("electricity" OR "electrical grid" OR "electrical infrastucture" OR (("energy" OR "power") NEAR/2 ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply" OR "electrical" OR "infrastructure" OR "grid" OR "grids" OR "technolog*" OR "energy system$" OR "power system$" OR "transition$" OR "policy" OR "policies" OR "clean" OR "cleaner" OR "decarboni*" OR "renewable" OR "green" OR "sustainable" OR "energy efficiency" )) ) )
```
Search #8
```
TS= ("SDG$ 7" OR "SDG7" OR "SDG-7" OR "sustainable development goal$ 7" OR (("sustainable development goal$" OR "SDG$" OR "goal 7" ) NEAR/15 "energy"))
```
Search #9
```
#5 NOT #6
```
Search #10
```
#9 OR #8 OR #7 OR #4 OR #3 OR #2 OR #1
```

</details>

## 2. General notes

Source of Targets and Indicators:
Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021]
<sup id="SDGT+Is">[1](#f1)</sup>

## 3. Targets

## Target 7.1

These targets are combined, as they cover similar topics.

> **7.1 By 2030, ensure universal access to affordable, reliable and modern energy services**
>
> 7.1.1 Proportion of population with access to electricity
>
> 7.1.2 Proportion of population with primary reliance on clean fuels and technology

This query consists of 5 phrases.

##### Phrase 1:

This phrase focuses on the clean fuels and technology part of the T&Is. Clean cooking is part of this, mentioned in the high level political forum document <sup id="HLPF2018">[2](#f2)</sup>. `solar cookers` are a type of clean cooking technology.

The second half of this phrase contains terms for various aspects:
* Usage rates and availability
* Barriers to increase
* Implementation
* Research concerning bringing technology to users
* Policy
* Incentives. Investment concerns target 7.A

```Ceylon =
TS=
(
  ("solar cooker$" OR "solar box cooker$"
  OR
    (
      ("clean" OR "cleaner" OR "decarboni*" OR "low-carbon")  
      NEAR/3
          ("fuel$" OR "energy" OR "power" OR "electricity"
          OR "technolog*"            
          OR "cooking" OR "stove$"
          )
    )
  )
  NEAR/15
      ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
      OR "access*" OR "availab*" OR "barrier$" OR "obstacle$"
      OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$"
      OR "implement*" OR "adopt*" OR "transition$"
      OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation"
      OR "policy" OR "policies" OR "legislation"
      OR "energy strateg*" OR "energy management" OR "energy planning"
      OR "feed-in tariff$" OR "market$" OR "initiative$"
      OR (("energy" OR "green") NEAR/2 "certificat*")
      OR "incentive$" OR "investment$" OR "investing" OR "invest"
      OR "sustainable development" OR "sustainable energy development"
      )
)
```
##### Phrase 2:

This phrase focuses on the universal and affordable access to electricity part of the T&Is. Papers discussing reliability and resilience of power grids are included. Some aspects about infrastructure also concern target 7.A/7.B.

`energy` and `power` are combined with other terms to avoid hits from other subject areas (biological energy, mechanical power). NEAR/2 is used as they should be almost next to each other.

*Comment 03092021 - note the typo in the second expression for infrastructure*

```Ceylon =
TS=
(
  ( "affordab*"
  OR "access*"
  OR "reliab*" OR "resilien*"
  OR "equitab*"
  OR
    ("infrastructure"
    NEAR/10  
        ("develop*" OR "upgrad*" OR "invest" OR "investment$" OR "investing" OR "modern*")
    )
  )
  NEAR/15
      ("electricity" OR "electrical grid" OR "electrical infrastucture"
      OR
        (
          ("energy" OR "power")
          NEAR/2
              ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply"
              OR "electrical"
              OR "infrastructure" OR "grid" OR "grids" OR "technolog*" OR "energy system$" OR "power system$"
              )            
        )
      OR
        (
          ("energy" OR "power" OR "electric" OR "electrical")
          NEAR/15
              ("microgrid" OR "microgrids" OR "micro-grid" OR "micro-grids")            
        )
      OR "off grid solution$"  
      )
)
```

##### Phrase 3:

`stable` and `stability` are very general words, so are combined with other terms here to reflect reliability.

The terms in the first expression are more specific so can be combined more loosely (`AND`) to electricity/energy.

*Comment 03092021 - note the typo in the second expression for infrastructure*

```Ceylon =
TS=
(
  ("stable supply" OR "supply stability" OR "grid stability"
  OR
    ("moderni*"
    NEAR/3
        ("energy" OR "power" OR "electricity" OR "grid" OR "grids")
    )    
  OR "sustainable development"    
  )
  AND
      ("electricity" OR "electrical grid" OR "electrical infrastucture"
      OR
        (
          ("energy" OR "power")
          NEAR/2
              ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply"
              OR "electrical"
              OR "infrastructure" OR "grid" OR "grids" OR "technolog*" OR "energy system$" OR "power system$"
              )            
        )
      OR "microgrid" OR "microgrids" OR "micro-grid" OR "micro-grids"
      OR "off grid solution$"  
      )
)
```

##### Phrase 4:

Access relates to energy poverty, security, justice etc.

```Ceylon =
TS=
(
  "universal electrification" OR "rural electrification"
  OR "energy security" OR "energy insecurity"
  OR "energy poverty" OR "energy vulnerability" OR "fuel poverty"
  OR "energy democracy" OR "energy justice"
)
```

##### Phrase 5:

Universal access, covering electrification of remote/rural regions. Least developed countries are likely to be relevant in the context of universal electrification and access for all. Lists of least developed countries, small island developing states and landlocked developing states are from the United Nations World Economic Situation and Prospects (tables F, H and I, pages 173-174)<sup id="UNLDCs">[3](#f3)</sup>.

```Ceylon =
TS=
(
  ("electrification" OR "electricity" OR "electrical supply"
  OR "energy service$" OR "energy access" OR "power supply"
  )
  NEAR/15
      (
        (
          ("remote" OR "rural")
          NEAR/3
              ("region$" OR "area" OR "areas" OR "communities" OR "community")
        )
      OR
        (
          "least developed"
          NEAR/3
              ("countr*" OR "state$" OR "nation$")
        )
      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"    
      )
)
```

## Target 7.2

> **7.2 By 2030, increase substantially the share of renewable energy in the global energy mix**
>
> 7.2.1 Renewable energy share in the total final energy consumption

This query consists of 2 phrases.

Search limited with terms that concern the changing of energy systems to renewables (incentives, policies), bringing of technology into use (commercialisation, scaling up) and measures that reflect the share of renewables. Basic research on renewable technology not included unless addresses these concepts around increasing the global share of renewables.

##### Phrase 1:

```Ceylon =
TS=
(
  "energy sector transformation"
  OR "renewable energy transition$" OR "national energy transition$"
  OR
    (
      ("share" OR "shares" OR "proportion$" OR "percentage$")
      NEAR/3
          ("renewables" OR "carbon-neutral" OR "green electricity" OR "green energy" OR "green power")
    )
)
```
##### Phrase 2:

The first half of this phrase contains terms for various aspects:
* Usage rates and availability
* Terms for global energy mix/supplies/markets/shares
* Barriers to increase
* Implementation. Here "transition" alone was too general so is combined.
* Research concerning bringing technology to users
* Policy
* Incentives

They are then combined with various types of renewable energy generation in the second expression. `solar energy` is combined with technological terms to prevent hits from astronomy. `biomass`, `wind` and `solar` combined with other terms to prevent hits from other subject areas.

Energy storage and smart grids to deal with fluctuations in supply are part of renewable energy transition (req. for renewables), inferred from the high level political forum document <sup id="HLPF2018">[2](#f2)</sup>.

```Ceylon =
TS=
(
  ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
  OR "access*" OR "availab*"
  OR
    (
      ("share" OR "shares" OR "proportion$" OR "percentage$")
      NEAR/2
          ("generat*" OR "service$" OR "sector" OR "production" OR "supply"
          OR "energy system$" OR "power system$" OR "global energy" OR "global electricity"
          )
    )
  OR "barrier$" OR "obstacle$"
  OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$"
  OR "implement*" OR "adopt*" OR "energy transition$" OR "renewable transition$" OR "transition* to" OR "pathway to"
  OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation"
  OR "policy" OR "policies" OR "legislation"
  OR "energy strateg*" OR "energy management" OR "energy planning"
  OR "kyoto protocol"
  OR "feed-in tariff$" OR "market$" OR "initiative$"
  OR (("energy" OR "green") NEAR/2 "certificat*")
  OR "incentive$" OR "investment$" OR "investing" OR "invest"
  OR "sustainable development" OR "sustainable energy development"
  )
  NEAR/15
      (
        (
          ("electricity" OR "power" OR "powered" OR "energy")
          NEAR/5
              ("renewable$"  OR "sustainable"
              OR "hydrothermal" OR "geothermal"
              OR "hydroelectric" OR "hydropower"
              OR "hydrokinetic"
              OR "hybrid" OR "carbon-neutral"
              OR "green electricity" OR "green energy" OR "green power"
              )    
        )
      OR "biofuel$" OR "bioenergy" OR "biodiesel"
      OR "solar cell$" OR "solar-cell$" OR "solar panel$" OR "solar-panel$" OR "solar power*"
      OR "solar array" OR OR "solar PV" OR "solar photovoltaic$"
      OR "solar thermal power" OR "solar thermal technolog*" OR "solar thermal collector$"
      OR "solar energy collector$" OR "solar district heating" OR "solar district cooling"
      OR "solar air heating system$" OR "solar space heating system$"
      OR
        ("solar thermal energy"
        NEAR/15
            ("power" OR "electric*" OR "water heating" OR "industrial process heat*")
        )
      OR "wind farm$" OR "wind turbine$"
      OR "tidal turbine$" OR "stream turbine$" OR "current turbine$"
      OR
        (
          ("biomass" OR "wind" OR "solar")
          NEAR/10
              ("electric*" OR "generat*" OR "service$" OR "sector" OR "produc*" OR "supply"
              OR "technolog*" OR "energy system$" OR "power system$"
              OR "energy crop$" OR "energy security"
              OR "biofuel$" OR "bioenergy" OR "biodiesel"
              )
        )
      OR ("hydrogen" NEAR/10 ("renewable substitute$" OR "renewable source$"))
      OR
        (
          ("fuel cell$" OR "battery" OR "batteries" OR "energy storage" OR "smart grid$")
          NEAR/15
              ("renewable" OR "sustainab*")
        )
      )
)
```


## Target 7.3

> **7.3 By 2030, double the global rate of improvement in energy efficiency**
>
> 7.3.1 Energy intensity measured in terms of primary energy and GDP

This query consists of 2 phrases.

##### Phrase 1:

The term "energy intensity" is combined with these other terms to prevent finding publications using the term in other contexts. Energy intensity definition from the European Environment Agency:
>"Energy intensity is the ratio between gross inland energy consumption (GIEC) and gross domestic product (GDP), calculated for a calendar year. GIEC is calculated as the sum of the gross inland consumption of the five sources of energy: solid fuels, oil, gas, nuclear and renewable sources" <sup id="EEA2016">[4](#f4)</sup>.

```Ceylon =
TS=
(
  ("energy intensity"
  AND
      ("energy consum*" OR "sustainab*" OR "energy efficiency"
      OR "GDP" OR "economic" OR "economy" OR "economies"
      OR "industry" OR "industrial" OR "manufacturing"
      OR ("emission$" NEAR/5 ("carbon" OR "co2"))
      OR "footprint$"
      OR "sustainable development"
      )
  )
  OR
  (
    ("economic growth" OR "GDP")
    NEAR/15
        ("energy use$" OR "energy consum*")
  )
)
```

##### Phrase 2:

Phrase 2 involves a `NOT` expression. This is to remove results concerning biological energy efficiency. Uses of `metabolism` as a term outside of biology are retained using a double negative `NOT` statement.

The first part includes mechanisms by which increases can be brought about.

```Ceylon =
TS=
(
  (
    (
      ("increas*" OR "improv*" OR "double" OR "enhanc*" OR "better" OR "more efficient" OR "higher"
      OR "policy" OR "policies" OR "legislation"
      OR "energy strateg*" OR "energy management" OR "energy planning"
      OR "initiative$"
      OR  (("energy" OR "green") NEAR/2 "certificat*")
      OR "incentive$" OR "investment$" OR "investing" OR "invest"
      OR "energy sustainability"
      )
      NEAR/15
          ("energy efficiency"
          OR "energy performance standard$"
          OR
            (
              ("energy efficien*" OR "energy saving")
              NEAR/10
                  ("housing" OR "houses" OR "residential" OR "building$" OR "cities"
                    OR "industry" OR "industrial" OR "manufacturing" OR "technolog*"
                  )
            )
          )
    )
  OR ("energy efficiency" NEAR/15 "sustainable development")
  )
  NOT
      ("caloric restriction" OR "calorie restriction" OR "metabolic syndrome"
      OR "muscle$" OR "mitochondria" OR "cardiovascular"
      OR "feed conversion" OR "animal energetics" OR "human energetics"
      OR
        (
          ("metabolism" OR "metabolic")
          NOT
              ("climate change" OR "economy" OR "economies"
              OR "social metabolism" OR "urban metabolism" OR "urban energy" OR "economic metabolism" OR "socioeconomic metabolism" OR "societal metabolism" OR "industrial metabolism" OR "carbon metabolism"
              )
        )
      )
)
```

## Target 7.a/7.b

> **7.a By 2030, enhance international cooperation to facilitate access to clean energy research and technology, including renewable energy, energy efficiency and advanced and cleaner fossil-fuel technology, and promote investment in energy infrastructure and clean energy technology**
>
> 7.a.1 International financial flows to developing countries in support of clean energy research and development and renewable energy production, including in hybrid systems
>
> **7.b By 2030, expand infrastructure and upgrade technology for supplying modern and sustainable energy services for all in developing countries, in particular least developed countries, small island developing States and landlocked developing countries, in accordance with their respective programmes of support**
>
> 7.b.1 Installed renewable energy-generating capacity in developing countries (in watts per capita)

This query consists of 1 phrase.

*Comment 03092021 - note the typo in the second expression for infrastructure*

```Ceylon =
TS=
(
  ("technical knowledge transfer" OR "transfer of technical knowledge" OR "transfer of technolog*" OR "technology transfer$"
  OR
    (
      ("research" OR "technology")
      NEAR/5 ("access*" OR "sharing" OR "shared benefit$")
    )  
  OR "capacity building" OR "build capacity" OR "capacity development"
  OR "international cooperation" OR "international collaboration" OR "foreign aid" OR "official development aid" OR "official development assistance"
  )
  NEAR/15
      ("electricity" OR "electrical grid" OR "electrical infrastucture"
      OR
        (
          ("energy" OR "power")
          NEAR/2
              ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply" OR "electrical"
              OR "infrastructure" OR "grid" OR "grids" OR "technolog*" OR "energy system$" OR "power system$"
              OR "transition$" OR "policy" OR "policies"
              OR "clean" OR "cleaner" OR "decarboni*" OR "renewable" OR "green" OR "sustainable" OR "energy efficiency"  
              )
        )        
      )
)
```

## General SDG

```Ceylon =
TS=
(
  "SDG$ 7" OR "SDG7" OR "SDG-7" OR "sustainable development goal$ 7"
  OR
    (
      ("sustainable development goal$" OR "SDG$" OR "goal 7" )
      NEAR/15 "energy"
    )
)
```

## Footnotes
<b id="f1">1</b> This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)".
(https://unstats.un.org/sdgs/indicators/indicators-list/) [↩](#SDGT+Is)

<b id="f2">2</b> UN (2018) 2018 HLPF Review of SDG implementation: SDG 7- Ensure access to affordable, reliable, sustainable and modern energy for all. https://sustainabledevelopment.un.org/content/documents/195532018_background_notes_SDG_7Final1.pdf. [↩](#HLPF2018)

<b id="f3">3</b> United Nations (2019) World Economic Situation and Prospects (Statistical Annex). https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<b id="f4">4</b> European Environment Agency (2016) Energy intensity. https://www.eea.europa.eu/data-and-maps/indicators/total-primary-energy-intensity-3 [↩](#EEA2016)
