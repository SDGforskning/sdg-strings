# Search query for SDG 7 - Affordable and clean energy, Bergen action-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 7
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes

## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 7</summary>

</details>

## 2. General notes

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021a](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Lists of least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) are from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) - countries were included if they appeared in the tables from 2016 to 2021 (i.e. were on these lists at any time between Nov 2015 and Dec 2020) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f2)</a>).

Other abbreviations:
* IEA - International Energy Agency
* EEA - European Environment Agency
* WHO - World Health Organization

## 3. Targets

## Target 7.1

> **7.1 By 2030, ensure universal access to affordable, reliable and modern energy services**
>
> 7.1.1 Proportion of population with access to electricity
>
> 7.1.2 Proportion of population with primary reliance on clean fuels and technology

This target is interpreted to cover research about:
* Access and reliance on clean vs. dirty fuels, and increasing use of clean fuels and clean technology in households (phrases 1-2). In v1 this target was interpreted more broadly to cover clean technologies generally, but the indicator metadata is about households, with focus on heating, lighting and cooking technologies (<a id="SDGindmetadata">[indicator 7.1.2, Statistics Division, 2021b](#f4)</a>).
* Affordable, reliable and modern electricity and energy services (phrases 3,4,5)
* Access to electricity and energy services (phrases 3 and 6)

<a id="IEAaccess">[IEA (2020)](#f5)</a> was used as a source of terms for this target, and as a reference for understanding "modern energy access":
>"There is no single internationally-accepted and internationally-adopted definition of modern energy access. Yet significant commonality exists across definitions, including: Household access to a minimum level of electricity; Household access to safer and more sustainable (i.e. minimum harmful effects on health and the environment as possible) cooking and heating fuels and stoves; Access to modern energy that enables productive economic activity, e.g. mechanical power for agriculture, textile and other industries; Access to modern energy for public services, e.g. electricity for health facilities, schools and street lighting." (IEA 2020)

This query consists of 6 phrases.

##### Phrase 1:

This phrase focuses on the clean fuels and technology part of the T&Is. The basic structure is *clean household energy activities + reliance/access*. Phrase 2 is similar, but adds some terms that need to be combined with `household$`. Adding `fuels OR technologies` as an additional element is too restrictive here - a number of works just talk about "clean cookstoves" for example.

Clean cooking is a central part of clean fuels/tech in this context (<a id="HLPF2018">[UN High level political forum on Sustainable Development, 2018](#f3)</a>). `solar cookers` are a type of clean cooking technology. The indicator metadata defines clean as:
> “Clean” is defined by the emission rate targets and specific fuel recommendations (i.e. against unprocessed coal and kerosene) included in the normative guidance WHO guidelines for indoor air quality: household fuel combustion. (<a id="SDGindmetadata">[indicator 7.1.2, Statistics Division, 2021b](#f4)</a>).

Within the WHO guidelines for indoor air quality (<a id="WHOair">[WHO, 2014, Executive summary and p.34-35](#f3)</a>), PM2.5 and carbon monoxide are identified in emissions targets, and unprocessed coal and kerosene should be avoided as fuels. Thus, while `decarboni*` was included in v1, it is removed in this version - carbon emissions do not seem to be the focus here under "clean". There are a large number of results lost by removing the ideas of decarbonisation and "clean technology" generally - consider including them in the topic/wide approach?

The second half of this phrase contains terms for various aspects to do with reliance, access and ways to increase usage, e.g.:
* Usage and access
* Barriers to increase
* Implementation
* Research concerning bringing technology to users
* Policies, incentives and investments

```Ceylon =
TS=
(
  ("solar cooker$" OR "solar box cooker$"
  OR "improved cookstove$" OR "improved stove$" OR "modern cookstove$" OR "modern stove$"
  OR
    (
      ("clean" OR "cleaner"
      OR "pm2.5" OR "fine particulate matter" OR "indoor air pollution"
      OR "unprocessed coal"
      )  
      NEAR/15
          ("cooking" OR "cookstove$" OR "stove$"
          OR "lighting" OR "lamps"
          OR "heating"
          )
    )
  )
  NEAR/15
      ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
      OR "access*" OR "availab*" OR "barrier$" OR "obstacle$"
      OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$"
      OR "implement*" OR "adopt*" OR "transition$" OR "intervention$"
      OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation"
      OR "policy" OR "policies" OR "legislation"
      OR "energy strateg*" OR "energy management" OR "energy planning"
      OR "feed-in tariff$" OR "market$" OR "initiative$"
      OR (("energy" OR "green") NEAR/2 "certificat*")
      OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
      OR "sustainable development" OR "sustainable energy development"
      )
)
```
##### Phrase 2

The basic structure is *clean fuels/tech + reliance/access + households*. It is similar to phrase 1, but includes terms such as `kerosene` og `fuel$` which are broad unless combined with `household$`.

```Ceylon =
TS=
(
  (
    ("clean" OR "cleaner" OR "modern"
    OR "pm2.5" OR "fine particulate matter" OR "indoor air pollution"
    OR "coal" OR "kerosene" OR "solid fuel$"
    )  
    NEAR/15
        ("fuel$" OR "energy" OR "electric*"
        OR "cooking" OR "cookstove$" OR "stove$"
        OR "lighting" OR "lamps"
        OR "heating"          
        )
    NEAR/15
        ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
        OR "access*" OR "availab*" OR "barrier$" OR "obstacle$"
        OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$"
        OR "implement*" OR "adopt*" OR "transition$" OR "intervention$"
        OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation"
        OR "policy" OR "policies" OR "legislation"
        OR "energy strateg*" OR "energy management" OR "energy planning"
        OR "feed-in tariff$" OR "market$" OR "initiative$"
        OR (("energy" OR "green") NEAR/2 "certificat*")
        OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
        OR "sustainable development" OR "sustainable energy development"
        )
  )    
  AND ("household$" OR "home$" OR "houses" OR "housing")      
)
```

##### Phrase 3

This phrase finds works about improving energy access and security. This phrase uses established phrases for these concepts; phrase 4 uses broader terms for affordability, and phrase 6 broader terms for access.

The general structure is *energy security/access phrases + action*. `increas*` is not used alone as there are many results using it talking about the results of e.g. energy povery.

```Ceylon =
TS=
(
  ("energy poverty" OR "energy vulnerability" OR "fuel poverty"
  OR "energy democracy" OR "energy justice"
  OR "energy security" OR "energy insecurity"
  )
  NEAR/5
      ("reduc*" OR "decreas*" OR "alleviat*" OR "address*"
      OR "combat" OR "fight*" OR "tackle"
      OR "improv*" OR "strengthen*"
      )
)
OR TS=("increas* energy security")
```

##### Phrase 4

This phrase finds works about affordable energy/electricity (in addition to phrase 3). The general structure is *affordable + energy*.

`energy` and `power` are combined with other terms to avoid results from other subject areas (biological energy, mechanical power).

```Ceylon =
TS=
(
  ("affordab*")
  NEAR/15
      ("energy service$" OR "electricity" OR "electrical energy"
      OR
        (
          ("energy" OR "power" OR "electric" OR "electrical")
          NEAR/3
              ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply")            
        )
      )
)
```

##### Phrase 5

This phrase to find research about modern or reliable energy services (in addition to phrase 3), as well as sustainable development of energy services.

`stable` and `stability` are very general words, so are combined with other terms. `microgrids` etc. are included as these are specific technologies used in areas which may not have access to a centralised power grid system.

```Ceylon =
TS=
(
  ("stable supply" OR "supply stability" OR "grid stability"
  OR "reliab*" OR "resilien*"
  OR
    ("modern*"
    NEAR/5
        ("energy" OR "electricity" OR "grid" OR "grids")
    )    
  OR "sustainable development"    
  )
  NEAR/15
      ("energy service$" OR "electricity" OR "electrical energy"
      OR
        (
          ("energy" OR "power" OR "electric" OR "electrical")
          NEAR/3
              ("generat*" OR "service$" OR "sector" OR "produc*" OR "supply"
              OR "infrastructure" OR "grid" OR "grids" OR "energy system$"
              )            
        )
      OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$"
      OR "off grid solution$" OR "off-grid system$"
      )
)
```

##### Phrase 6

This phrase is about universal access, covering electrification of remote/rural regions. The general structure is *universal electrification / access + energy  / access + energy + regions*. Least developed countries are included regions. `energy services` is considered specialised enough to stand alone with `access`, while `electricity` and `energy` are too broad (can be used in many contexts). Thus these terms are combined either in phrases, or with regions, or with certain technologies (e.g. `microgrids`).

```Ceylon =
TS=
(
  "universal electrification" OR "rural electrification"
  OR
    ("access"
    NEAR/5
      ("energy service$")
    )
  OR
    ("access"
    NEAR/15
      ("electricity" OR "energy")
    NEAR/15
      ("microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$"
      OR "off grid solution$" OR "off-grid system$"
      )
    )
)
OR
TS=
(
  ("electrification" OR "energy access" OR "grid extension$"
  OR
    (
      ("access" OR "provide$" OR "provision")
      NEAR/5
          ("electrical supply" OR "power supply" OR "electricity" OR "energy service$")
    )  
  )
  NEAR/15
      ("rural"
      OR
        ("remote"
        NEAR/3 ("region$" OR "area" OR "areas" OR "communities" OR "community")
        )
      OR
        ("least developed"
        NEAR/3 ("countr*" OR "state$" OR "nation$")
        )
      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"    
      )
)
```

## Target 7.2

> **7.2 By 2030, increase substantially the share of renewable energy in the global energy mix**
>
> 7.2.1 Renewable energy share in the total final energy consumption

This target is interpreted to cover research about increasing the use of renewable energy. This includes research about the transition of energy systems to renewables (e.g. research discussing transitions, access, incentives, policies), bringing of technology into use (e.g. commercialisation, scaling up) and research measuring usage of renewables (e.g. reliance on it, how large share does it have). Basic research on renewable energy technology is not included, unless it also discusses increasing the global share (or mechanisms to).

This query consists of 2 phrases.

##### Phrase 1

This phrase covers established phrases around transitioning to renewable energy.

```Ceylon =
TS=
(
  "energy sector transformation"
  OR "renewable energy transition$" OR "national energy transition$"
)
```

##### Phrase 2

The general structure of this phrase is *transitions/shares/incentives etc. + renewable energy*. The first part contains terms for various aspects, such as:
* Usage
* Global energy mix/supplies/shares
* Support and barriers
* Implementation. Here "transition" alone was too general so is combined.
* Research concerning bringing technology to users
* Policies, incentives and investments

In the renewable energy terms, `biomass`, `wind` and `solar` are generally combined with other terms to prevent results from other subject areas (e.g. astronomy). Energy storage and smart grids to deal with fluctuations in supply can be considered part of renewable energy transition (<a id="HLPF2018">[UN High level political forum on Sustainable Development, 2018](#f3)</a>).

```Ceylon =
TS=
(
  ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
  OR
    (
      ("share" OR "shares" OR "proportion$" OR "percentage$")
      NEAR/5
          ("generat*" OR "service$" OR "sector" OR "production" OR "supply" OR "supplies"
          OR "global energy" OR "global electricity" OR "energy mix"
          )
    )
  OR "barrier$" OR "obstacle$"
  OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$"
  OR (("promot*" OR "support*" OR "encourag*") NEAR/5 "renewable$")
  OR "implement*" OR "adopt*" OR "energy transition$" OR "renewable transition$" OR "transition* to"
  OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation"
  OR "policy" OR "policies" OR "legislation" OR "kyoto protocol"
  OR "energy strateg*" OR "energy management" OR "energy planning"
  OR "feed-in tariff$" OR "market$" OR "initiative$"
  OR (("energy" OR "green") NEAR/2 "certificat*")
  OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
  OR "sustainable development" OR "sustainable energy development"
  )
  NEAR/15
      (
        (
          ("electricity" OR "power" OR "powered" OR "energy")
          NEAR/5
              ("renewable$"  OR "sustainable"
              OR "hydrothermal" OR "geothermal"
              OR "hydroelectric" OR "hydro electric" OR "hydropower" OR "hydro power"
              OR "hydrokinetic"
              OR "hybrid" OR "carbon-neutral"
              OR "green electricity" OR "green energy" OR "green power"
              )    
        )
      OR "biofuel$" OR "bioenergy" OR "biodiesel"
      OR "solar cell$" OR "solar-cell$" OR "solar panel$" OR "solar-panel$" OR "solar power*"
      OR "solar array" OR "solar PV" OR "solar photovoltaic$"
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

This target is interpreted to cover:
* Research about improving energy intensity (phrase 1)
* Research about improving energy efficiency and measures/interventions to improve efficiency

Energy intensity definition from the European Environment Agency:
>"Energy intensity is the ratio between gross inland energy consumption (GIEC) and gross domestic product (GDP), calculated for a calendar year. GIEC is calculated as the sum of the gross inland consumption of the five sources of energy: solid fuels, oil, gas, nuclear and renewable sources" (<a id="EEA2016">[EEA, 2016](#f6)</a>).

This query consists of 2 phrases.

##### Phrase 1

This phrase finds research about improving energy intensity; the general structure is *energy intensity + action + energy terms*. The *energy terms* contains terms that help avoid publications using "energy intensity" in other contexts.

The *action terms* include a number of mechanisms by which changes can be brought about, such as investments and incentives (as in other targets of this SDG), but also terms for mechanisms specific for energy efficiency, such as `energy labelling` (<a id="IEAenergylabelling">[IEA, 2021](#f7)</a>).

```Ceylon =
TS=
(
  ("energy intensity"
  NEAR/10
      ("reduc*" OR "decreas*" OR "lower"
      OR "improv*" OR "enhanc*" OR "better" OR "more efficient"
      OR "policy" OR "policies" OR "legislation"
      OR "energy strateg*" OR "energy management" OR "energy planning"
      OR "initiative$" OR "intervention$"
      OR  (("energy" OR "green") NEAR/2 "certificat*")
      OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
      OR "energy sustainability"
      OR "minimum energy performance" OR "energy labelling" OR "energy standard$" OR "energy efficiency standard$"
      OR "sustainable development"
      )
  )
  AND
      ("energy consum*" OR "sustainab*" OR "energy efficiency"
      OR "GDP" OR "economic" OR "economy" OR "economies"
      OR "industry" OR "industrial" OR "manufacturing"
      OR "policy" OR "policies"
      OR ("emission$" NEAR/5 ("carbon" OR "co2"))
      OR "footprint$"
      OR "sustainable development"
      )
)
```

##### Phrase 2

This phrase finds research about increasing energy efficiency. The general structure is *action + energy efficiency + sectors / action + energy efficiency*. As "energy efficiency" can be used in other subject areas (e.g. biology, medicine) it is either a) combined with various sectors/items processes that account for energy use (first part), or b) used only with action terms that are relevant to the energy sector (second part).

The *action terms* include a number of mechanisms by which changes can be brought about, such as investments and incentives (as in other targets of this SDG), but also terms for mechanisms specific for energy efficiency, such as `energy labelling` (<a id="IEAenergylabelling">[IEA, 2021](#f7)</a>).

*sector terms* were built around generic terms (e.g. `residential` will find "residential water heating"), and supplemented with terms from the IEA webpages and IEAs energy efficiency indicators manual (<a id="IEAmanual">[IEA, 2014](#f8)</a>). Household consumption sources (p. 40), service sector terms (p. 69) and transport terms (p. 128) were taken from this manual, but not all (e.g. `buses` removed due to being used in context with voltages; including specific industries (e.g. steel) did not improve results). `lighting`, `applicances`, `data centres` and `data networks` were added as they have their own recent efficiency tracking reports from the IEA (https://www.iea.org/analysis/all?topic=energy-efficiency&type=report). `smart` is a very general term, but when paired with energy efficiency finds many different types of system/device (smart windows, grids, thermostats etc.).

```Ceylon =
TS=
(
    (
      ("increas*" OR "improv*" OR "double" OR "enhanc*" OR "better" OR "more efficient" OR "higher"
      OR "policy" OR "policies" OR "legislation"
      OR "energy strateg*" OR "energy management" OR "energy planning"
      OR "initiative$" OR "intervention$"
      OR  (("energy" OR "green") NEAR/2 "certificat*")
      OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
      OR "energy sustainability"
      OR "minimum energy performance" OR "energy labelling" OR "energy standard$" OR "energy efficiency standard$"
      OR "sustainable development"
      )
      NEAR/15
            ("energy efficien*" OR "energy saving")
      NEAR/15
            ("housing" OR "houses" OR "homes" OR "household" OR "domestic" OR "residential" OR "building$" OR "cities"
            OR "service sector" OR "office$" OR "retail" OR "food services" OR "restaurants" OR "hotels" OR "warehouses"
            OR "lighting" OR "lamps" OR "cooking" OR "appliances" OR "white goods"
            OR "plug-in device$" OR "smart"
            OR "space cooler$" OR "air condition*" OR "space heat*" OR "room heating" OR "district heating" OR "heat pump$" OR "HVAC"
            OR "industry" OR "industrial" OR "manufacturing" OR "technolog*"
            OR "transport" OR "transportation" OR "vehicles" OR "cars" OR "train$" OR "airplane$" OR "aeroplane$" OR "ship$" OR "shipping" OR "freight"
            OR "telecomm*" OR "data centre$" OR "data center$" OR "data network$" OR "server" OR "servers" OR "wireless"
            )
    )
  OR
    ("energy efficiency"
    NEAR/15
        ("policy" OR "policies" OR "framework$" OR "legislation"
        OR "energy strateg*" OR "energy management" OR "energy planning"
        OR "initiative$" OR "intervention$"
        OR  (("energy" OR "green") NEAR/2 "certificat*")
        OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
        OR "energy sustainability"
        OR "minimum energy performance" OR "energy labelling" OR "energy standard$" OR "energy efficiency standard$"
        OR "sustainable development"
        )
    )
)
```

*OLD FORMAT KEPT TO BE USED/ADAPTED IN TOPIC APPROACH* - As energy efficiency cant be used alone

Involves a `NOT` expression. This is to remove results concerning biological energy efficiency. Uses of `metabolism` as a term outside of biology are retained using a double negative `NOT` statement.

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
      OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
      OR "energy sustainability"
      OR "minimum energy performance" OR "energy labelling" OR "energy standard$" OR "energy efficiency standard$"
      )
      NEAR/15
          ("energy efficiency"
          OR
            (
              ("energy efficien*" OR "energy saving")
              NEAR/15
                  ("housing" OR "houses" OR "homes" OR "household" OR "domestic" OR "residential" OR "building$" OR "cities"
                  OR "service sector" OR "office$" OR "retail" OR "food services" OR "restaurants" OR "hotels" OR "warehouses"
                  OR "lighting" OR "lamps" OR "cooking" OR "appliances" OR "white goods" OR "plug-in device$" OR "smart"
                  OR "space cooler$" OR "air condition*" OR "space heat*" OR "room heating" OR "district heating" OR "heat pump$" OR "HVAC"
                  OR "industry" OR "industrial" OR "manufacturing" OR "technolog*"
                  OR "transport" OR "transportation" OR "vehicles" OR "cars" OR "train$" OR "airplane$" OR "aeroplane$" OR "ship$" OR "shipping" OR "freight"
                  OR "telecomm*" OR "data centre$" OR "data center$" OR "data network$" OR "server" OR "servers" OR "wireless"
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

## Target 7.a

> **7.a By 2030, enhance international cooperation to facilitate access to clean energy research and technology, including renewable energy, energy efficiency and advanced and cleaner fossil-fuel technology, and promote investment in energy infrastructure and clean energy technology**
>
> 7.a.1 International financial flows to developing countries in support of clean energy research and development and renewable energy production, including in hybrid systems

This target is interpreted to cover research about a) international cooperation for clean energy research and technology, b) access to clean energy research and technology, and c) investment in clean energy research and technology (all phrase 1), and d) investment in energy infrastructure (inc. renewables; phrase 2). Here, "clean" is interpreted to include also low-carbon due to the specific mention of cleaner fossil fuel technologies in the target.

##### Phrase 1

The general structure is *sharing/investing/cooperation + clean energy/tech*. Major forms of renewable energy are included. 

```Ceylon =
TS=
(
  ("transfer of technolog*" OR "technology transfer$"
  OR
    ("knowledge transfer"
    NEAR/3 ("technolog*" OR "technical")
    )
  OR
    (
      ("research" OR "technology" OR "technologies" OR "innovation$")
      NEAR/5
          ("access*" OR "sharing" OR "shared benefit$"
          OR "capacity building" OR "build* capacity" OR "capacity development"
          )
    )  
  OR "international cooperation" OR "international collaboration"
  OR "foreign aid" OR "official development aid" OR "official development assistance"
  OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
  )
  NEAR/15
      ("cleantech"
      OR
        (
          ("technolog*" OR "innovation$")
          NEAR/3
              ("clean" OR "cleaner" OR "green" OR "greener"
              OR "decarboni*" OR "low carbon" OR "energy efficiency"  
              OR "renewable$" OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower"
              )
        )      
      OR
        (
          ("research*")
          NEAR/3
              ("energy" OR "electricity" OR "fuel" OR "fuels")
          NEAR/3
              ("clean" OR "cleaner" OR "green" OR "greener"
              OR "decarboni*" OR "low carbon" OR "renewable$"
              OR "energy efficiency"  
              OR "transition$" OR "policy" OR "policies"
              )
        )  
      )             
)
```

##### Phrase 2

The general structure is *investment + energy infrastructure/renewable energy*. Major forms of renewable energy are included. 

```Ceylon =
TS=
(
  ("foreign aid" OR "official development aid" OR "official development assistance"
  OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
  )
  NEAR/15
      ("energy service$" OR "energy sector"
      OR "electrical infrastructure"
      OR "electrical grid$" OR "power grid$" OR "grid extension$" OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$" OR "smart grid$"
      OR "energy storage system$"
      OR
        (
          ("energy" OR "electricity")
          NEAR/5
              ("generation" OR "infrastructure" OR "access"
              OR "renewable$" OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower"
              )
        )             
      )
)
```

## Target 7.b

> **7.b By 2030, expand infrastructure and upgrade technology for supplying modern and sustainable energy services for all in developing countries, in particular least developed countries, small island developing States and landlocked developing countries, in accordance with their respective programmes of support**
>
> 7.b.1 Installed renewable energy-generating capacity in developing countries (in watts per capita)

This target is interpreted to cover research about improving infrastructure and technologies for sustainable and modern energy services in developing countries (with a focus on LDCs, SIDS and LDSs). Modern energy is defined in 7.1. This query consists of 1 phrase. Specific LDCs, SIDS and LDSs are included as terms.

```Ceylon =
TS=
(
  (
    ("improv*" OR "increas*" OR "strengthen*" OR "enhanc*" OR "better"
    OR "more efficient" OR "upgrad*" OR "scal* up" OR "build*" OR "expand" OR "accelerat*"
    )  
    NEAR/5  
      ("energy service$" OR "energy sector"
      OR "electrical infrastructure"
      OR "electrical grid$" OR "power grid$" OR "grid extension$" OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$" OR "smart grid$"
      OR "energy storage system$"
      OR
        (
          ("energy" OR "electricity")
          NEAR/5
              ("generation" OR "infrastructure" OR "technolog*"
              OR "access" OR "off grid"
              OR "renewable$" OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower")
        )             
      )
  )
  AND  
      ("least developed countr*" OR "least developed nation$"
      OR "developing countr*" OR "developing nation$" OR "developing states"

      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"

      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "St Lucia" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa" OR "Sao Tome" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "Tuvalu" OR "Vanuatu" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"

      OR "Afghanistan" OR "Armenia" OR "Azerbaijan" OR "Bhutan" OR "Bolivia" OR "Botswana" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "Ethiopia" OR "Kazakhstan" OR "Kyrgyzstan" OR "Kyrgyz Republic" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "Mali" OR "Mongolia" OR "Nepal" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova" OR "Rwanda" OR "South Sudan" OR "Swaziland" OR "Tajikistan" OR "Turkmenistan" OR "Uganda" OR "Uzbekistan" OR "Zambia" OR "Zimbabwe"
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

## 4. Authorship and review

## 5. Footnotes

<a id="f6"></a> EEA .(2016). *Energy intensity*. https://www.eea.europa.eu/data-and-maps/indicators/total-primary-energy-intensity-3 [↩](#EEA2016)

<a id="f8"></a> IEA. (2014). *Energy Efficiency Indicators: Fundamentals on Statistics*. https://www.iea.org/reports/energy-efficiency-indicators-fundamentals-on-statistics [accessed 7th Jan 2022] [↩](#IEAmanual)

<a id="f5"></a> IEA. (2020, 13th October). *Defining energy access: 2020 methodology*. https://www.iea.org/articles/defining-energy-access-2020-methodology [accessed 7th Jan 2022] [↩](#IEAaccess)

<a id="f7"></a> IEA. (2021). *Appliances and Equipment*. https://www.iea.org/reports/appliances-and-equipment [accessed 7th Jan 2022] [↩](#IEAenergylabelling)

<a id="f1"></a> Statistics Division. (2021a). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f4"></a> Statistics Division. (2021b). *SDG Indicators Metadata Repository*. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/metadata/ [accessed 8 December 2021] [↩](#SDGindmetadata)

<a id="f2"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f3">2</a> UN High level political forum on Sustainable Development. (2018). *2018 HLPF Review of SDG implementation: SDG 7- Ensure access to affordable, reliable, sustainable and modern energy for all*. https://sustainabledevelopment.un.org/content/documents/195532018_background_notes_SDG_7Final1.pdf [Accessed 06.01.2022] (#HLPF2018)
