# Search query for SDG 7 - Affordable and clean energy, Bergen action-approach.

**Current status**: This string is being edited after internal review - expect changes. It is substantially changed from the original version it was based on (v2019.11).

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

This target uses various descriptive terms for energy services, technologies and fuels. For the purpose of these search strings, we are operating using the following definitions:

* Modern energy services: We consider this to mainly refer to electrification and reliance on clean fuels/technology. <a id="IEAaccess">[IEA (2020)](#f5)</a> was used as a reference for understanding "modern energy access":
>"There is no single internationally-accepted and internationally-adopted definition of modern energy access. Yet significant commonality exists across definitions, including: Household access to a minimum level of electricity; Household access to safer and more sustainable (i.e. minimum harmful effects on health and the environment as possible) cooking and heating fuels and stoves; Access to modern energy that enables productive economic activity, e.g. mechanical power for agriculture, textile and other industries; Access to modern energy for public services, e.g. electricity for health facilities, schools and street lighting." (IEA 2020)

* Sustainable energy services: These are only mentioned in 7.b, and we interpret this to be the same as "modern".

* Renewable energy: We consider this to cover energy (e.g. electricity, heating) from sources that are renewable. We do not include "low-carbon" finite sources or "cleaner fossil fuel technology" in this category.

* Clean fuels/technology: We consider this to cover fuels and technology that do not release, or reduce the release of, pollution that directly harms humans. This could include cleaner fossil-fuel/ non-renewable sources, as well as renewable energy (but not e.g. biomass burning that produces household air pollution). It does not automatically include decarbonised technologies. This is based on the 7.1.2 indicator metadata, which links "clean" to indoor air quality, and the examples given in target 7.a:
> “Clean” is defined by the emission rate targets and specific fuel recommendations (i.e. against unprocessed coal and kerosene) included in the normative guidance WHO guidelines for indoor air quality: household fuel combustion. (<a id="SDGindmetadata">[indicator 7.1.2, Statistics Division, 2021b](#f4)</a>).

> "[...] access to clean energy research and technology, including renewable energy, energy efficiency and advanced and cleaner fossil-fuel technology [...]" (target 7.a)

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
* Increasing access to and primary use of clean fuels and clean technology in households (phrases 1 & 2). Clean cooking is a central part of clean fuels/tech in this context (<a id="HLPF2018">[UN High level political forum on Sustainable Development, 2018](#f3)</a>). In v2019.11 this target was interpreted more broadly to cover clean technologies generally, but the indicator metadata is about households, with focus on heating, lighting and cooking technologies (<a id="SDGindmetadata">[indicator 7.1.2, Statistics Division, 2021b](#f4)</a>).
* Reducing the use of non-clean fuels in households (phrase 3)
* Improving access to modern energy services, including electricity. This includes concepts such as energy justice, energy security and fuel poverty (phrases 4 & 5)
* Improving the affordability and reliability of energy services (phrase 6)

<a id="IEAaccess">[IEA (2020)](#f5)</a> and <a id="UNThemereport">[UN (2021)](#f9)</a> were used as a source of terms for this target. This query consists of 6 phrases.

##### Phrase 1
The basic structure is *clean fuels/tech + action + households*. The action part of this phrase contains terms for various aspects to do with increasing reliance, access and uptake, e.g. interventions, policy, investing and reducing barriers. *Household terms* are included as terms such as `fuel$` are broad. "Clean technology" in household contexts should be covered by `clean` NEAR `cooking`, `fuels` etc. or by the general term `energy transition$`.

```Ceylon =
TS=
(
  (
    (
      ("energy transition$"
      NEAR/5 ("household$" OR "cooking" OR "stove$" OR "lighting" OR "lamps" OR "heating")
      )
    OR
      (
        ("clean*" OR "modern*")
        NEAR/5
            ("fuel$" OR "energ*" OR "electric*"
            OR "cooking" OR "stove$" OR "lighting" OR "lamps" OR "heating"
            )
      )
    )
    NEAR/15
        ("implement*" OR "adopt*" OR "establish*" OR "transition*"
        OR "intervention$" OR "initiative$" OR "upscale" OR "scale-up"
        OR "encourag*" OR "incentive$" OR "investing" OR "invest" OR "subsidi*"
        OR
          (
            ("increas*" OR "improv*" OR "facilitate" OR "expand*" OR "expansion")
            NEAR/5
                ("relian*" OR "uptake" OR "use" OR "usage" OR "primary source$"
                OR "access*" OR "availab*" OR "attractive*"
                OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$"
                OR "commercial development" OR "develop* commercially" OR "commerciali?ation" OR "investment$"
                )
          )
        OR (("reduc*" OR "remov*" OR "address") NEAR/5 ("barrier$" OR "obstacle$"))
        OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning"
        OR "feed-in tariff$" OR (("energy" OR "green") NEAR/2 "certificat*")
        OR "sustainable development" OR "sustainable energy development"
        )
  )    
  AND ("household$" OR "home$" OR "house" OR "houses" OR "housing" OR "room"
      OR "residential" OR "dwelling$" OR "domestic" OR "slum$" OR "community" OR "village$" OR "women")      
)
```
##### Phrase 2:

The basic structure is *clean household energy activities + action*. It is similar to phrase 1, but the terms used here are more specific (e.g. `solar cookers`) so do not require "household" terms.

```Ceylon =
TS=
(
  ("solar cooker$" OR "solar box cooker$" OR "solar cooking"
  OR "improved cookstove$" OR "improved stove$" OR "modern cookstove$" OR "modern stove$"
  )
  NEAR/15
      ("implement*" OR "adopt*" OR "establish*" OR "transition*"
      OR "intervention$" OR "initiative$" OR "upscale" OR "scale-up"
      OR "encourag*" OR "incentive$" OR "investing" OR "invest" OR "subsidi*"
      OR
        (
          ("increas*" OR "improv*" OR "facilitate" OR "expand*" OR "expansion")
          NEAR/5
              ("relian*" OR "uptake" OR "use" OR "usage" OR "primary source$"
              OR "access*" OR "availab*" OR "attractive*"
              OR "economic feasibility" OR "cost-effectiveness" OR "affordab*" OR "cost-advantage$"
              OR "commercial development" OR "develop* commercially" OR "commerciali?ation" OR "investment$"
              )
        )
      OR (("reduc*" OR "remov*" OR "address") NEAR/5 ("barrier$" OR "obstacle$"))
      OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning"
      OR "feed-in tariff$" OR (("energy" OR "green") NEAR/2 "certificat*")
      OR "sustainable development" OR "sustainable energy development"
      )
)
```

##### Phrase 3:

The basic structure is *"dirty" fuels + action*. It is similar to phrase 1, but the negative side (e.g. phasing out). Within the WHO guidelines for indoor air quality (<a id="WHOair">[WHO, 2014, Executive summary and p.34-35](#f3)</a>), PM2.5 and carbon monoxide are identified in emissions targets, and unprocessed coal and kerosene should be avoided as fuels. Searching for coal + heating is challenging as lots of industrial results, hence the two parts of this phrase.

```Ceylon =
TS=
(
  (
    ("kerosene" OR "solid fuel$" OR "coal")
    NEAR/15
        ("transition*" OR "intervention$" OR "initiative$"
        OR "encourag*" OR "incentive$" OR "investing" OR "invest"
        OR "reduc*" OR "decreas*" OR "prevent" OR "mitigat*" OR "phase out"
        OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning"
        OR "feed-in tariff$" OR (("energy" OR "green") NEAR/2 "certificat*")
        OR "sustainable development" OR "sustainable energy development"
        )
  )    
  NEAR/15 ("household$" OR "home$" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic use*" OR "slum$" OR "village$" OR "women"
      OR "residential heating" OR "central heating" OR "winter heating" OR "cooking" OR "stove$" OR "lighting" OR "lamps")      
)
OR
TS=
(
  ("coal"
  NEAR/5
      ("transition*" OR "coal to electricity" OR "intervention$" OR "initiative$"
      OR "encourag*" OR "incentive$" OR "investing" OR "invest"
      OR "phase out"
      OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning"
      OR "feed-in tariff$" OR (("energy" OR "green") NEAR/2 "certificat*")
      OR "sustainable development" OR "sustainable energy development"
      )
  )    
  NEAR/15
      ("household$" OR "home$" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic use*" OR "slum$" OR "village$" OR "women"
      OR "heating" OR "cooking" OR "stove$" OR "lighting" OR "lamps"
      )      
)
```

##### Phrase 4

This phrase finds works about improving energy access and security. This phrase uses established phrases for these concepts; phrase 5 uses broader terms for affordability, and phrase 7 broader terms for access.

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

##### Phrase 5

This phrase is about universal access, covering electrification of remote/rural regions. The general structure is *universal electrification / action + access + energy  / action + access + energy + regions*. The reason for the two part approach is that `energy services` is specialised enough to stand alone with `access`, while `electricity` and `energy` are too broad (can be used in many contexts, e.g. an industrial process). Thus these terms are combined either in phrases, or with regions, or with certain technologies (e.g. `microgrids`). Regions include least economically developed countries and rural areas.

```Ceylon =
TS= ("universal electrification" OR "rural electrification" OR "national electrification")
OR
TS=
(
  (
    ("improv*" OR "increas*" OR "ensur*")
    NEAR/5 ("access" OR "provision")  
  )
  NEAR/5
      ("energy service$" OR "electricity supply"
      OR
        (
          ("energy" OR "power" OR "electric*")
          NEAR/3
              ("household$" OR "home$" OR "house" OR "houses" OR "housing"
              OR "residential" OR "dwelling$" OR "domestic use*" OR "slum$" OR "village$"
              OR "sustainable"
              )            
        )
      )
)
OR
TS=
(
  ("electrification" OR "grid extension$"
  OR
    (
      (
        ("improv*" OR "increas*" OR "ensur*")
        NEAR/5 ("access" OR "provision")
      )
      NEAR/5 ("electrical supply" OR "power supply" OR "electricity")
    )
  )
  NEAR/15
      ("rural"
      OR
        (
          ("remote")
          NEAR/3 ("region$" OR "area" OR "areas" OR "communities" OR "community")
        )
      OR
        ("least developed" NEAR/3 ("countr*" OR "state$" OR "nation$")
        )
      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"    
      )
)
```

##### Phrase 6

This phrase finds works about improving affordability and reliability of energy services. The general structure is *action + afford/stable + energy*. in the action terms, `reduce` is not truncated due to chemical reduction. In the energy terms, `energy` and `power` are combined with other terms to avoid results from other subject areas (biological energy, mechanical power). `microgrids` etc. are included as these are specific technologies used in areas which may not have access to a centralised power grid system.
```Ceylon =
TS=
(
  (
    (
      ("improv*" OR "increas*" OR "ensur*")
      NEAR/5
      ("stable" OR "stability" OR "reliab*" OR "resilien*" OR "afford*")  
    )
    OR
    (
      ("reduc*" OR "decreas*" OR "improv*" OR "prevent")
      NEAR/5
      ("unstable" OR "instability" OR "unreliab*" OR "unafford*" OR "costly" OR "expensive")  
    )
  )
  NEAR/15
      ("energy service$" OR "electricity supply"
      OR
        (
          ("energy" OR "power" OR "electric*")
          NEAR/3
              ("household$" OR "home$" OR "house" OR "houses" OR "housing"
              OR "residential" OR "dwelling$" OR "domestic use*" OR "slum$" OR "village$"
              OR "sustainable"
              )            
        )
      OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$"
      OR "off grid solution$" OR "off-grid system$"
      )
)
```

## Target 7.2

> **7.2 By 2030, increase substantially the share of renewable energy in the global energy mix**
>
> 7.2.1 Renewable energy share in the total final energy consumption

This target is interpreted to cover research about increasing the use of renewable energy. This includes research about the transition of energy systems to renewables (e.g. research discussing transitions, access, incentives, policies), research about increasing the use/share, research about bringing of technology into use (e.g. commercialisation, scaling up, investment), and research about reducing reliance on fossil fuels. Basic research on renewable energy technology is not included, unless it also discusses increasing the global share (or mechanisms to increase it).

This query consists of 3 phrases.

##### Phrase 1

This phrase covers the general terms of transitioning and transforming to renewable energy. "energy transition" is not used alone as this does not necessarily mean renewables (e.g. one can talk about historical energy transitions from wood to steam).

```Ceylon =
TS=
("renewable"
  NEAR/5 ("energy transition$" OR "sector transformation$" OR "energy transformation$")
)
```

##### Phrase 2

This phrase covers specific terms for increasing the share of renewable energy, including a wider set of terms for renewables. The general structure is *action/transitions/promotional mechanisms + renewable energy*.

The "promotional mechanisms" include several aspects, such as Incentives and barriers; Policies, incentives and investments; Economic mechanisms; Research concerning bringing technology to users; Sustainable development. `adopting OR adoption` is used as "adopted" is used often as a verb in methods; `increase` is used rather than "increas*" as a number of technical works begin with the technical issue of "increasing proportions of renewables in the power grid".

In the *renewable energy terms*, `biomass`, `wind` and `solar` are generally combined with other terms to prevent results from other subject areas (e.g. astronomy). Energy storage and smart grids to deal with fluctuations in supply can be considered part of renewable energy transition (<a id="HLPF2018">[UN High level political forum on Sustainable Development, 2018](#f3)</a>).

```Ceylon =
TS=
(
  (
    (
      ("increase" OR "improv*" OR "enhanc*" OR "promot*" OR "support" OR "encourag*")
      NEAR/5
          ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
          OR "contribution" OR "proportion" OR "share" OR "expansion"
          OR "affordab*" OR "investment$"
          OR "energy service$" OR "energy sector"
          OR "global energy" OR "global electricity" OR "energy mix"
          )
    )
  OR "implement*" OR "adopting" OR "adoption"
  OR "energy transition$" OR "renewable transition$" OR "transition* to"
  OR "incentive$" OR "initiative$"
  OR (("energy" OR "green") NEAR/2 "certificat*")
  OR "barrier$" OR "obstacle$"
  OR "policy" OR "policies" OR "legislation" OR "kyoto protocol" OR "strateg*" OR "energy management" OR "energy planning"
  OR "subsidi*" OR "economic feasibility" OR "cost-effectiveness" OR "cost-advantage$"
  OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
  OR "feed-in tariff$" OR "market$"
  OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "commerciali?ation"
  OR "sustainable development" OR "sustainable energy development"
  )
  NEAR/15
      (
        (
          ("electricity" OR "power" OR "powered" OR "energy")
          NEAR/5
              ("renewable$"  OR "sustainable"
              OR "hydrothermal" OR "geothermal"
              OR "hydroelectric" OR "hydropower" OR "hydro"
              OR "hydrokinetic"
              OR "green"
              )    
        )
      OR "geothermal health pump$" OR "ground source heat pump$"
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
      OR "biofuel$" OR "bioenergy" OR "biodiesel"
      OR
        (
          ("biomass" OR "wind" OR "solar")
          NEAR/10
              ("electric*" OR "generat*" OR "service$" OR "sector"
              OR "technolog*" OR "energy system$" OR "power system$"
              OR "energy crop$" OR "energy security"
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

##### Phrase 3

This phrase covers reduction in fossil fuels. The general structure is *action + fossil fuels + reliance/energy mix*. `oil` is not linked to consumption due to results from medicine (e.g. fish oil).

```Ceylon =
TS=
(
  (
    ("reduce" OR "decreas*" OR "phase out" OR "phasing out"
    OR "improv*" OR "incentiv*" OR "support" OR "encourag*"
    OR "transition*" OR "intervention$"
    OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning"
    )
    NEAR/5
        ("fossil fuel$" OR "coal" OR "oil")
  )
  NEAR/15
    ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
    OR "coal consumption" OR "fossil fuel consumption" OR "consumption of fossil fuel$"
    OR "energy service$" OR "energy sector" OR "energy supply" OR "energy supplies"
    OR "global energy" OR "global electricity" OR "energy mix"
    )
)   
```

## Target 7.3

> **7.3 By 2030, double the global rate of improvement in energy efficiency**
>
> 7.3.1 Energy intensity measured in terms of primary energy and GDP

This target is interpreted to cover:
* Research about improving energy intensity (phrase 1,2)
* Research about improving energy efficiency and measures/interventions to improve efficiency (phrase 3)

Energy intensity definition from the European Environment Agency:
>"Energy intensity is the ratio between gross inland energy consumption (GIEC) and gross domestic product (GDP), calculated for a calendar year. GIEC is calculated as the sum of the gross inland consumption of the five sources of energy: solid fuels, oil, gas, nuclear and renewable sources" (<a id="EEA2016">[EEA, 2016](#f6)</a>).

This query consists of 3 phrases.

##### Phrase 1

This phrase finds research about improving energy intensity. The general structure is *energy intensity + action + energy terms*.

The *energy terms* contains terms that help avoid publications using "energy intensity" in other contexts. The *action terms* include a number of mechanisms by which changes can be brought about, such as investments and incentives (as in other targets of this SDG), but also terms for mechanisms specific for energy efficiency, such as `energy labelling` (<a id="IEAenergylabelling">[IEA, 2021](#f7)</a>).

```Ceylon =
TS=
(
  ("energy intensity"
  NEAR/5
      ("reduc*" OR "decreas*" OR "lower"
      OR "improv*" OR "enhanc*" OR "better" OR "more efficient"
      OR "policy" OR "policies" OR "legislation" OR "strateg*" OR "management" OR "planning" OR "plan" OR "plans"
      OR "initiative$" OR "intervention$"
      OR "incentive$" OR "investment$" OR "investing" OR "invest" OR "green bond$" OR "climate bond$"
      OR  (("energy" OR "green") NEAR/2 "certificat*")
      OR "minimum energy performance" OR "energy labelling" OR "energy standard$" OR "energy efficiency standard$"
      OR "sustainable development" OR "energy sustainability"
      )
  )
  AND
      ("energy consum*" OR "sustainab*" OR "energy efficiency"
      OR "GDP" OR "economic" OR "economy" OR "economies"
      OR "industry" OR "industrial" OR "manufacturing"
      OR ("emission$" NEAR/5 ("carbon" OR "co2"))
      OR "footprint$"
      )
)
```

##### Phrase 2
This phrase covers research about energy intensity via the decoupling of energy consumption and economic growth. The general structure is *energy consumption + action + economy*.

```Ceylon =
TS=
(
  ("energy consum*"
  NEAR/5 ("decouple*" OR "de couple*")
  )
    NEAR/5 ("econom*" OR "GDP")
)
```

##### Phrase 3

This phrase finds research about increasing energy efficiency. The general structure is *energy efficiency/loss + action + sectors* OR *energy efficiency + action*. As "energy efficiency" can be used in other subject areas (e.g. biology, medicine) it is either a) combined with various sectors/items processes that account for energy use (first part), or b) used only with action terms that are relevant to the energy sector (second part, with varying NEAR distances).

*sector terms* were built around generic terms (e.g. `residential` will find "residential water heating"), and supplemented with terms from the IEA webpages and IEAs energy efficiency indicators manual (<a id="IEAmanual">[IEA, 2014](#f8)</a>). Household consumption sources (p. 40), service sector terms (p. 69) and transport terms (p. 128) were taken from this manual, but not all (e.g. `buses` removed due to being used in context with voltages; including specific industries (e.g. steel) did not improve results). `lighting`, `applicances`, `data centres` and `data networks` were added as they have their own recent efficiency tracking reports from the IEA (https://www.iea.org/analysis/all?topic=energy-efficiency&type=report). `smart` is a very general term, but when paired with energy efficiency finds many different types of system/device (smart windows, grids, thermostats etc.).

The *action terms* include a number of mechanisms by which changes can be brought about, such as investments and incentives (as in other targets of this SDG), but also terms for mechanisms specific for energy efficiency, such as `energy labelling` (<a id="IEAenergylabelling">[IEA, 2021](#f7)</a>). `increase$ OR increasing` is used to avoid "increasingly".

```Ceylon =
TS=
(
    (
      (
        (
          ("energy efficien*" OR "energy utili$ation efficiency" OR "energy saving")
          NEAR/5
              ("increase$" OR "increasing" OR "improv*" OR "double" OR "enhanc*" OR "better" OR "more efficient" OR "higher")
        )
        OR ("energy loss" NEAR/5 ("reduc*" OR "decreas*" OR "limit" OR "prevent*"))
      )
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
    ( "energy efficiency"
      NEAR/5
          ("policy" OR "policies" OR "framework$" OR "legislation" OR "strateg*" OR "management" OR "planning" OR "plan" OR "plans"
          OR "initiative$" OR "intervention$"
          OR "incentive$" OR "investment$" OR "investing" OR "invest"
          )
    )
    OR
    ( "energy efficiency"
      NEAR/15
          ((("energy" OR "green") NEAR/2 "certificat*")
          OR "green bond$" OR "climate bond$"
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

* V2 edit (Oct-Feb 2022): CSA
* Internal review (Mar 2022): HMB, ML
* Terminology workshop with specialists (Apr 2022):

## 5. Footnotes

<a id="f6"></a> EEA .(2016). *Energy intensity*. https://www.eea.europa.eu/data-and-maps/indicators/total-primary-energy-intensity-3 [↩](#EEA2016)

<a id="f8"></a> IEA. (2014). *Energy Efficiency Indicators: Fundamentals on Statistics*. https://www.iea.org/reports/energy-efficiency-indicators-fundamentals-on-statistics [accessed 7th Jan 2022] [↩](#IEAmanual)

<a id="f5"></a> IEA. (2020, 13th October). *Defining energy access: 2020 methodology*. https://www.iea.org/articles/defining-energy-access-2020-methodology [accessed 7th Jan 2022] [↩](#IEAaccess)

<a id="f7"></a> IEA. (2021). *Appliances and Equipment*. https://www.iea.org/reports/appliances-and-equipment [accessed 7th Jan 2022] [↩](#IEAenergylabelling)

<a id="f1"></a> Statistics Division. (2021a). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f4"></a> Statistics Division. (2021b). *SDG Indicators Metadata Repository*. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/metadata/ [accessed 8 December 2021] [↩](#SDGindmetadata)

<a id="f2"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f9"></a> United Nations. (2021). *Theme Report on Energy Access* [Executive summary, Background document]. High-level Dialogue on Energy
New York, September 2021. https://www.un.org/en/conferences/energy2021/RESOURCES [Accessed 03.03.2022]. [↩](#UNThemereport)

<a id="f3"></a> UN High level political forum on Sustainable Development. (2018). *2018 HLPF Review of SDG implementation: SDG 7- Ensure access to affordable, reliable, sustainable and modern energy for all*. https://sustainabledevelopment.un.org/content/documents/195532018_background_notes_SDG_7Final1.pdf [Accessed 06.01.2022]
