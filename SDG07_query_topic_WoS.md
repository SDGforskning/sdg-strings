# Search query for SDG 7 - Affordable and clean energy, Bergen topic-approach.

**Current status**: This string is currently a finished version (1.0.0).

**Contents**

1. Full query in copy-pasteable format
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes

## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here: https://www.webofscience.com/wos/woscc/summary/d154b0d3-89dc-465a-84c8-ec84a0fe5854-57bae169/relevance/1 (no filters; all years)

## 2. General notes

This document contains search strings for finding publications related to the topics in SDG 7 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in SDG 7 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

This target uses various terms for categories of energy services, technologies and fuels (e.g. "renewable", "clean", "modern"). This presents two challenges: 1) Interpreting exactly what types of services/technologies these refer to, and 2) matching this up with how researchers actually use these terms in their work. Our understanding is that researchers from different traditions, subject areas or political alignments may prefer/avoid certain terms, or define them differently (for example, some might say nuclear is "renewable" while others would disagree; whether natural gas is "green"; whether one prefers the term "low carbon" to "renewable"). For the latter challenge, we try to use a range of terms, but without going too far outside what we consider most people to mean by the term. For the first challenge, we have used sources from large international agencies/the UN to interpret the language of the SDG, and we are using the following definitions:

* **Modern energy services**: We consider this to refer to services which meet energy needs based on **clean fuels/technology** (see below for definition of this). Electrification is an important type. <a id="IEAaccess">[IEA (2020)](#f5)</a> was used as a reference for understanding "modern energy access":
>"There is no single internationally-accepted and internationally-adopted definition of modern energy access. Yet significant commonality exists across definitions, including: Household access to a minimum level of electricity; Household access to safer and more sustainable (i.e. minimum harmful effects on health and the environment as possible) cooking and heating fuels and stoves; Access to modern energy that enables productive economic activity, e.g. mechanical power for agriculture, textile and other industries; Access to modern energy for public services, e.g. electricity for health facilities, schools and street lighting." (IEA 2020)

* **Renewable energy**: We consider this to cover energy (e.g. electricity, heating) from sources that are renewable. We do not include "low-carbon" finite sources, "cleaner fossil fuel technology" or nuclear energy in this category. This decision is based on information from the UN SDG Indicators metadata repository, which for 7.2.1 (which concerns "renewable energy") does not include any of these types, and says the following:
> "A number of definitions of renewable energy exist; what they have in common is highlighting as renewable all forms of energy that their consumption does not deplete their availability in the future. These include solar, wind, ocean, hydropower, geothermal sources, and bioenergy (in the case of bioenergy, which can be depleted, sources of bioenergy can be replaced within a short to medium-term frame)". (<a id="SDGindmetadata">[indicator 7.2.1, Statistics Division, 2021b](#f4)</a>).

* **Clean fuels/technology**: We consider this to cover fuels and technology that do not release, or reduce the release of, pollution that directly harms humans. This could include cleaner fossil-fuel or non-renewable sources, as well as renewable energy (but not e.g. biomass burning that produces household air pollution). It does not automatically include decarbonised technologies. These decisions are based on the 7.1.2 indicator metadata, which links the term  "clean" to indoor air quality, and the examples given in target 7.a which include "cleaner fossil-fuel technology":
> “Clean” is defined by the emission rate targets and specific fuel recommendations (i.e. against unprocessed coal and kerosene) included in the normative guidance WHO guidelines for indoor air quality: household fuel combustion. (<a id="SDGindmetadata">[indicator 7.1.2, Statistics Division, 2021b](#f4)</a>).

> "[...] access to clean energy research and technology, including renewable energy, energy efficiency and advanced and cleaner fossil-fuel technology [...]" (target 7.a)

* **Sustainable energy services**: These are only mentioned in 7.b, and we interpret this to be the same as "modern".

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021a](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f2)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

Other abbreviations:
* IEA - International Energy Agency
* EEA - European Environment Agency
* WHO - World Health Organization

## 3. Targets

### Target 7.1

> **7.1 By 2030, ensure universal access to affordable, reliable and modern energy services**
>
> 7.1.1 Proportion of population with access to electricity
>
> 7.1.2 Proportion of population with primary reliance on clean fuels and technology

This target is interpreted to cover research about:
* Clean fuels and clean technology in households (phrases 1 & 2). Clean cooking is a central part of clean fuels/tech in this context (<a id="HLPF2018">[UN High level political forum on Sustainable Development, 2018](#f3)</a>). In v2019.11 this target was interpreted more broadly to cover clean technologies generally, but the indicator metadata is about households, with focus on heating, lighting and cooking technologies (<a id="SDGindmetadata">[indicator 7.1.2, Statistics Division, 2021b](#f4)</a>).
* Non-clean fuels in households (phrase 3)
* Access to modern energy services, including electricity. This includes concepts such as energy justice, energy security and fuel poverty (phrases 4 & 5)
* The affordability, stability, and reliability of energy services (phrase 6)

<a id="IEAaccess">[IEA (2020)](#f5)</a> and <a id="UNThemereport">[UN (2021)](#f9)</a> were used as a source of terms for this target. This query consists of 6 phrases.

#### Phrase 1
The elements of the phrase are: *energy transitions/clean fuels/tech + households*. *Household terms* are included as terms such as `fuel$` are broad. Compared to the action approach, a couple of terms were removed as they created noise (`home OR community`). "Clean technology" in household contexts should be covered by the terms for `cooking`, `stove$`, `fuels` etc. or by the general term `energy transition$`.

```py
TS=
(
  (
    ("energy transition$" NEAR/5 ("household$" OR "cooking" OR "stove$" OR "lighting" OR "lamps" OR "heating"))
    OR
      (
        ("clean*" OR "modern*")
        NEAR/5
            ("fuel$" OR "energ*" OR "electric*"
            OR "cooking" OR "stove$" OR "lighting" OR "lamps" OR "heating"
            )
      )
  )    
  AND ("household$" OR "homes" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic" OR "slum$" OR "village$" OR "women"
      )      
)
```
#### Phrase 2

The elements of the phrase are: *clean household energy activities*. It is similar to phrase 1, but the terms used here are more specific (e.g. `solar cookers`) so do not require "household" terms.

```py
TS=
(
  "solar cooker$" OR "solar box cooker$" OR "solar cooking"
  OR "improved cookstove$" OR "improved stove$" OR "modern cookstove$" OR "modern stove$"
)
```

#### Phrase 3

The elements of the phrase are: *"dirty" fuels + households*. It is similar to phrase 1, but the negative side (e.g. phasing out). Within the WHO guidelines for indoor air quality (<a id="WHOair">[WHO, 2014, Executive summary and p.34-35](#f3)</a>), PM2.5 and carbon monoxide are identified in emissions targets, and unprocessed coal and kerosene should be avoided as fuels. Searching for coal + heating is challenging as lots of industrial results, hence the two parts of this phrase. The household terms are slightly edited compared to the action string to reduce noise (`slum OR slums`, and removed `village$`).

```py
TS=
(
  ("kerosene" OR "solid fuel$" OR "coal"
  )    
  NEAR/15
      ("household$" OR "homes" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic use*" OR "slum" OR "slums" OR "women"
      OR "residential heating" OR "central heating" OR "winter heating" OR "cooking" OR "stove$" OR "lighting" OR "lamps"
      )      
)
OR
TS=
(
  ("coal")    
  NEAR/15
      ("household$" OR "homes" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic use*" OR "slum" OR "slums" OR "women"
      OR "heating" OR "cooking" OR "stove$" OR "lighting" OR "lamps"
      )      
)
```

#### Phrase 4

This phrase finds works about energy access and security. This phrase uses established phrases for these concepts; other phrases use broader terms for affordability and access.

The elements of the phrase are: *energy security/access phrases*. `energy NEAR/3 (dignity OR care)` was tested but there were few relevant results at this time in this combination.

```py
TS=
(
  "energy poverty" OR "energy vulnerability" OR "fuel poverty"
  OR "energy democracy" OR "energy justice" OR "energy inequity"
  OR "energy security" OR "energy insecurity"
)
```

#### Phrase 5

This phrase is about access to energy services and electricity. The elements of the phrase are: *electrification / access + energy + households / access + energy + regions*. The reason for the two part approach is that `energy services` is specialised enough to stand alone with `access`, while `electricity` and `energy` are too broad (can be used in many contexts, e.g. an industrial process). Thus these terms are combined either in phrases, or with regions, or with certain technologies (e.g. `microgrids`). For *regions*, we include generic terms for developing, least developed countries and rural areas, as well as specific least developed countries, SIDS, landlocked developing countries.

```py
TS= ("universal electrification" OR "rural electrification" OR "national electrification")
OR
TS=
(
  ("access" OR "provision")
  NEAR/5
      ("energy service$" OR "electricity supply"
      OR
        (
          ("energy" OR "power" OR "electric*")
          NEAR/3
              ("household$" OR "home$" OR "house" OR "houses" OR "housing"
              OR "residential" OR "dwelling$" OR "domestic use*" OR "slum$" OR "village$"
              OR "sustainable" OR "green" OR "clean" OR "modern"
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
      ("access" OR "provision")
      NEAR/5 ("energy" OR "electricity" OR "electrical supply" OR "power supply")
    )
  )
  NEAR/15
      ("rural"
      OR ("remote" NEAR/3 ("region$" OR "area" OR "areas" OR "communities" OR "community"))
      OR "least developed countr*" OR "least developed nation$"
      OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
      OR "less developed countr*" OR "less developed nation$"
      OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
      OR "underserved countr*" OR "underserved nation$"
      OR "deprived countr*" OR "deprived nation$"
      OR "middle income countr*" OR "middle income nation$"
      OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
      OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
      OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
      OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
      )
)
```

#### Phrase 6

This phrase finds works about affordability and reliability of energy services. The elements of the phrase are: *afford/stable + energy*. In the energy terms, `energy` and `power` are combined with other terms to avoid results from other subject areas (biological energy, mechanical power). `microgrids` etc. are included as these are specific technologies used in areas which may not have access to a centralised power grid system.

```py
TS=
(
  ("stable" OR "stability" OR "reliab*" OR "resilien*" OR "afford*" OR "inexpensive" OR "low cost" OR "cheap"
  OR "unstable" OR "instability" OR "unreliab*" OR "unafford*" OR "costly" OR "energy cost$" OR "expensive"
  )
  NEAR/15
      ("energy service$" OR "electricity supply"
      OR
        (
          ("energy" OR "power" OR "electric*")
          NEAR/5
              ("household$" OR "home$" OR "house" OR "houses" OR "housing"
              OR "residential" OR "dwelling$" OR "domestic use*" OR "slum" OR "slums" OR "village$"
              OR "sustainable"
              )            
        )
      OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$"
      OR "off grid solution$" OR "off-grid system$"
      OR (("energy" OR "electricity") NEAR/3 ("infrastructure" OR "off grid" OR "decentrali$ed" OR "cooperative$"))
      OR "community energy" OR "community renewable energy"
      )
)
```

### Target 7.2

> **7.2 By 2030, increase substantially the share of renewable energy in the global energy mix**
>
> 7.2.1 Renewable energy share in the total final energy consumption

One could interpret this target in two ways according to the topic approach:
1. This target is interpreted to cover research about the use and uptake of renewable energy, or
2. This target is interpreted to cover research about renewable energy. 
These two different interpretations make a large difference to the number of results, given (2) will find a large number of technical publications about renewable energy technology (gives ca. 3.5x the number of results as interpretation (1)). For the moment, we have decided to use interpretation (1). This means that the strings attempt to find publications focusing on renewable energy use and uptake, including works that talk about the share, transitions, policies, commercialisation, scaling up, and investment in renewable energy, and research about reliance on and consumption of fossil fuels.

This query consists of 3 phrases.

#### Phrase 1

This phrase covers the general terms of transitioning and transforming to renewable energy. The elements of the phrase are: *renwables + energy transitions/transformations/substitutions*. "energy transition" is not used alone as this does not necessarily mean renewables (e.g. one can talk about historical energy transitions from wood to steam). Compared to the action approach, a wider distance is used between elements.

```py
TS=
(
  ("renewable" AND ("energy transition$" OR "sector transformation$" OR "energy transformation$"))
  OR ("renewable energy" NEAR/15 ("substitut*" OR "uptake"))
)
```

#### Phrase 2

This phrase covers terms renewable energy. The elements of the phrase are: *use/share/adoption/investing/barriers/promotional actions + renewable energy*.

In the *renewable energy terms*, `biomass`, `wind` and `solar` are generally combined with other terms to prevent results from other subject areas (e.g. astronomy) - these have been narrowed slightly in the topic approach compared to the action approach (particularly biomass was causing issues). Energy storage and smart grids to deal with fluctuations in supply can be considered part of renewable energy transition (<a id="HLPF2018">[UN High level political forum on Sustainable Development, 2018](#f3)</a>). We include the term `green` energy/power etc. - a potential problem is that some may use this term very widely to include non-renewables (see discussion under "General Notes"). However a test demonstrated that this is not a large issue - of over 1200 results referring to green energy/power/electricity, only around 35 referred to "natural gas" and 30 to "nuclear".

```py
TS=
(
  ("relian*" OR "primary use" OR "primary usage" OR "primary source$" OR "adopting" OR "adoption" OR "implementation" OR "uptake" 
  OR "contribution" OR "proportion" OR "share" OR "expansion"
  OR "feasibility" OR "attractiveness" OR "incentive$" OR "initiative$"
  OR "affordab*" OR "inexpensive" OR "low cost" OR "economic feasibility" OR "economic viability" OR "cost-effectiveness" OR "cost-advantage$"
  OR "investment$" OR "subsidies" OR "subsidi$ation" OR "financing" OR "funding" OR "commerciali?ation"
  OR "energy service$" OR "energy sector" OR "generation" OR "capacity"
  OR "global energy" OR "global electricity" OR "energy mix" OR "market share$"
  OR "barrier$" OR "obstacle$"
  OR "implement" OR "adopt" OR "incentivi*"
  OR "energy transition$" OR "renewable transition$" OR "transition* to"
  OR ("certificat*" NEAR/2 ("energy" OR "green"))
  OR "policy" OR "policies" OR "legislation" OR "kyoto protocol" OR "strateg*" OR "energy management" OR "energy planning"
  OR "subsidi$e" OR "investing" OR "invest" OR "green bond$" OR "climate bond$" OR "feed-in tariff$"
  OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "roll out" OR "rollout"
  OR "sustainable development" OR "sustainable energy development"
  )
  NEAR/15
      ("non conventional energy"
      OR
        (
          ("electricity" OR "power" OR "powered" OR "energy")
          NEAR/5
              ("renewable$"  OR "sustainable" OR "green"
              OR "hydrothermal" OR "geothermal"
              OR "hydroelectric" OR "hydropower" OR "hydro"
              OR "hydrokinetic"
              )    
        )
      OR "geothermal heat pump$" OR "ground source heat pump$"
      OR "solar cell$" OR "solar-cell$" OR "solar panel$" OR "solar-panel$" OR "solar power*" OR "solar array" OR "solar PV" OR "solar photovoltaic$"
      OR "solar energy collector$" OR "solar farm$" OR "solar plant$" OR "solar park$"
      OR "solar district heating" OR "solar district cooling" OR "solar air heating system$" OR "solar space heating system$"
      OR ("solar thermal" NEAR/3 ("power" OR "technolog*" OR "collector$" OR "district"))
      OR ("solar thermal energy" NEAR/15 ("power" OR "electric*" OR "water heating" OR "industrial process heat*"))
      OR "wind farm$" OR "wind turbine$" OR "wind park$" OR "wind factory" OR "wind factories"
      OR "tidal turbine$" OR "stream turbine$" OR "current turbine$"
      OR "tidal power" OR "tidal energy" OR "marine energy"
      OR ("wave energy" NEAR/5 ("converter$" OR "renewable" OR "power" OR "generat*" OR "energy harvesting"))
      OR "biofuel$" OR "bioenergy" OR "biodiesel"
      OR
        (
          ("biomass" OR "wind" OR "solar" OR "ammonia")
          NEAR/10
              ("electric*" OR "energy generat*" OR "energy service$" OR "energy sector"
              OR "energy system$" OR "power system$"
              OR "energy crop$" OR "energy security"
              )
        )
      OR ("hydrogen" NEAR/10 ("renewable substitute$" OR "renewable source$" OR "green"))
      OR
        (
          ("fuel cell$" OR "battery" OR "batteries" OR "lithium ion" OR "energy storage" OR "smart grid$")
          NEAR/15 ("renewable" OR "sustainab*")
        )
      )
)
```

#### Phrase 3

This phrase covers reliance on and consumption of fossil fuels. The elements of the phrase are: *fossil fuels + reliance/energy mix*. Action terms are retained for "oil" because it is used to generally (e.g. consuption of fish oil, reliance of technology for oil drilling etc.)

```py
TS=
(
  ("fossil fuel$" OR "coal" OR "natural gas" OR "grey hydrogen" OR "conventional energy"
  OR
    (
      ("reduce" OR "decreas*" OR "phase out" OR "phasing out"
      OR "improv*" OR "incentiv*" OR "support" OR "encourag*"
      OR "transition*" OR "substitut*" OR "intervention$"
      OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning"
      )
      NEAR/5
          ("oil")
    )
  )
  NEAR/15
    ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
    OR "coal consumption" OR "fossil fuel consumption" OR "consumption of fossil fuel$"
    OR "energy service$" OR "energy sector" OR "energy supply" OR "energy supplies"
    OR "global energy" OR "global electricity" OR "energy mix"
    )
)   
```

### Target 7.3

> **7.3 By 2030, double the global rate of improvement in energy efficiency**
>
> 7.3.1 Energy intensity measured in terms of primary energy and GDP

This target is interpreted to cover research about energy intensity (phrase 1,2), and research about energy efficiency (phrase 3). While some might consider a reduction in energy consumption, or degrowth, to be essential to sustainable energy, the target is specifically about energy efficiency. Therefore we held our interpretation within this theme for the action approach. However, for the topic approach, we include the concepts of `energy conservation` (phrase 3) and `energy sufficiency` (phrase 4), given that they are closely tied to efficiency, as well as energy justice which is a theme in this SDG.

Energy intensity definition from the European Environment Agency:
>"Energy intensity is the ratio between gross inland energy consumption (GIEC) and gross domestic product (GDP), calculated for a calendar year. GIEC is calculated as the sum of the gross inland consumption of the five sources of energy: solid fuels, oil, gas, nuclear and renewable sources" (<a id="EEA2016">[EEA, 2016](#f6)</a>).

This query consists of 3 phrases.

#### Phrase 1

This phrase finds research about improving energy intensity. The elements of the phrase are: *energy intensity + energy terms*.

The *energy terms* contains terms that help avoid publications using "energy intensity" in other contexts.

```py
TS=
(
  ("energy intensity")
  AND
      ("energy consum*" OR "sustainab*" OR "energy efficiency"
      OR "GDP" OR "economic" OR "economy" OR "economies"
      OR "industry" OR "industrial" OR "manufacturing"
      OR ("emission$" NEAR/5 ("carbon" OR "co2"))
      OR "footprint$"
      )
)
```

#### Phrase 2
This phrase covers research about energy intensity via the decoupling of energy consumption and economic growth. The elements of the phrase are: *energy consumption + action + economy*. This action needs to be retained for the context, since energy intensity is about the coupling of energy consumption with GDP.

```py
TS=
(
  ("energy consum*"
  NEAR/5 ("decoupl*" OR "de coupl*")
  )
  NEAR/5 ("econom*" OR "GDP")
)
```

#### Phrase 3

This phrase finds research about energy efficiency. The elements of the phrase are: *energy efficiency/loss + sectors* OR *energy efficiency + action*. As "energy efficiency" can be used in other subject areas (e.g. biology, medicine) it is either a) combined with various sectors/items processes that account for energy use (first part), or b) used only with action terms that are relevant to the energy sector (second part, with varying NEAR distances). These actions are retained even in this topic approach, because without them energy efficiency is too broad/noisy.

*sector terms* were built around generic terms (e.g. `residential` will find "residential water heating"), and supplemented with terms from the IEA webpages and IEAs energy efficiency indicators manual (<a id="IEAmanual">[IEA, 2014](#f8)</a>). Household consumption sources (p. 40), service sector terms (p. 69) and transport terms (p. 128) were taken from this manual, but not all (e.g. `buses` removed due to being used in context with voltages; including specific industries (e.g. steel) did not improve results). `lighting`, `applicances`, `data centres` and `data networks` were added as they have their own recent efficiency tracking reports from the IEA (https://www.iea.org/analysis/all?topic=energy-efficiency&type=report). `smart` is a very general term, but when paired with energy efficiency finds many different types of system/device (smart windows, grids, thermostats etc.).

The *action terms* include a number of mechanisms by which changes can be brought about, such as investments and incentives (as in other targets of this SDG), but also terms for mechanisms specific for energy efficiency, such as `energy labelling` (<a id="IEAenergylabelling">[IEA, 2021](#f7)</a>). `increase$ OR increasing` is used to avoid "increasingly".

```py
TS=
(
    (
      ("energy efficien*" OR "energy utili$ation efficiency" OR "energy saving" OR "energy loss" OR "energy conservation")
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
      (("energy efficiency" OR "energy conservation")
      NEAR/5
            ("policy" OR "policies" OR "framework$" OR "legislation" OR "management" OR "planning" OR "plan" OR "plans"
            OR "initiative$" OR "intervention$" OR "incentive$" OR "investment$" OR "investing" OR "invest"
            )
      )
    OR
      ("energy efficiency"
      NEAR/15
            ("green bond$" OR "climate bond$"
            OR ("certificat*" NEAR/2 ("energy" OR "green"))
            OR "energy sustainability"
            OR "minimum energy performance" OR "energy labelling" OR "energy standard$" OR "energy efficiency standard$"
            OR "sustainable development"
            )
      )
)
```

#### Phrase 4

This phrase covers energy sufficiency. The elements of the phrase are: *energy sufficiency + energy terms*

```py
TS=
  ("energy sufficiency"
  AND
      ("electric*" OR "energy generat*" OR "energy service$" OR "energy sector" OR "energy system$"
      OR "power system$" OR "energy security" OR "renewable energy"
      )
  )
```

### Target 7.a

> **7.a By 2030, enhance international cooperation to facilitate access to clean energy research and technology, including renewable energy, energy efficiency and advanced and cleaner fossil-fuel technology, and promote investment in energy infrastructure and clean energy technology**
>
> 7.a.1 International financial flows to developing countries in support of clean energy research and development and renewable energy production, including in hybrid systems

This target is interpreted to cover research about:
* international cooperation for clean energy research and technology (phrase 1)
* access to clean energy research and technology, in part via transfers of technology between sectors/actors (phrase 1)
* investment in clean energy research and technology, here we include development assistance (phrase 1)
* investment in energy infrastructure (phrase 2).

Here, "clean" is interpreted to include also low-carbon due to the specific mention of cleaner fossil fuel technologies in the target. All phrases also include `energy transition$` as this term incorporates many of the aspects around modernised and cleaner energy supplies/infrastructure/tech.

This target consists of 2 phrases.

#### Phrase 1
The elements of the phrase are: *sharing/investing/cooperation + clean energy research/tech*.

```py
TS=
(
  ("ODA" OR "development spending" OR "cooperation fund"
  OR  
    (
      ("international" OR "development" OR "foreign")
      NEAR/3
          ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
          OR "aid" OR "assistance"
          OR "fund$" OR "grant$" OR "financing" OR "financial resources" OR "capital flow$"
          )
    )
  OR  
    (
      ("knowledge" OR "technolog*" OR "technical" OR "research" OR "scientific" OR "R&D")
      NEAR/5 ("access*" OR "capacity" OR "transfer" OR "sharing" OR "shared" OR "share" OR "cooperat*" OR "co-operat*" OR "collaborat*" OR "partnership$")
    )
  OR "invest" OR "investing" OR "investment$" OR "financing" OR "funding" OR "financial resources"
  OR (("financial*" or "monetary") NEAR/3 ("support*" or "assist*"))
  OR "economic support" OR "economic assistance"
  OR "green bond$" OR "climate bond$"
  )
  NEAR/15
      ("cleantech" OR "energy research" OR "energy efficiency research" OR "energy transition$" OR "energy technolog*"
      OR
        (
          ("technolog*" OR "innovation$" OR "R&D")
          NEAR/3
              ("clean" OR "cleaner" OR "green" OR "greener"
              OR "decarboni*" OR "low carbon" OR "energy efficien*"  
              OR "renewable$" OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower" OR "marine energy" OR "tidal energy" OR "wave energy"
              )
        )      
      )             
)
```

#### Phrase 2

The elements of the phrase are: *investment + energy infrastructure/renewable energy*.

```py
TS=
(
  ("ODA" OR "development spending" OR "cooperation fund"
  OR  (
        ("international" OR "development" OR "foreign")
        NEAR/3
            ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
            OR "aid" OR "assistance"
            OR "fund$" OR "grant$" OR "financing" OR "financial resources" OR "capital flow$"
            )
      )
  OR "invest" OR "investing" OR "investment$" OR "financing" OR "funding" OR "financial resources"
  OR (("financial*" or "monetary" OR "economic") NEAR/3 ("support*" or "assist*" OR "resources"))
  OR "green bond$" OR "climate bond$"  
  )
  NEAR/15
      ("energy service$" OR "energy sector" OR "electrical infrastructure" OR "electricity supply" OR "power supply"
      OR (("energy" OR "electricity") NEAR/5 ("infrastructure" OR "technolog*" OR "off grid" OR "decentrali$ed" OR "cooperative$"))
      OR "community energy" OR "community renewable energy"
      OR "electrical grid$" OR "power grid$" OR "grid extension$" OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$" OR "smart grid$" OR "energy storage system$"
      OR "energy transition$"
      OR
        (
          ("power station$" OR "power generation" OR "energy generation" OR "generator$")
          NEAR/5
              ("modern" OR "clean" OR "sustainable" OR "renewable$" OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower" OR "marine" OR "tidal" OR "wave energy")
        )             
      )            
)
```

### Target 7.b

> **7.b By 2030, expand infrastructure and upgrade technology for supplying modern and sustainable energy services for all in developing countries, in particular least developed countries, small island developing States and landlocked developing countries, in accordance with their respective programmes of support**
>
> 7.b.1 Installed renewable energy-generating capacity in developing countries (in watts per capita)

This target is interpreted to cover research about infrastructure for sustainable and modern energy services in developing countries. The focus is on infrastructure and supply. We interpret this to cover electricity generation, power grids, storage, and energy services. The general structure is *action/modern/sustainable + infrastructure/technology/services + developing countries*. This string has been converted from the topic approach by retaining the action terms, but adding to them to additionally include works generally talking about modern and sustainable services.

```py
TS=
(
  (
    ("modern*" OR "clean" OR "sustainable" OR "renewable$" OR "decarboni*" OR "low carbon"
    OR "improv*" OR "increas*" OR "strengthen*" OR "enhanc*" OR "better"
    OR "more efficient" OR "upgrad*" OR "scal* up"
    OR "build" OR "expand*" OR "extend*" OR "deploy" OR "accelerat*" OR "prioriti$e"
    OR "energy sector transform*"
    )  
    NEAR/5  
      ("energy service$" OR "energy sector" OR "electrical infrastructure" OR "electricity supply" OR "power supply"
      OR (("energy" OR "electricity") NEAR/5 ("infrastructure" OR "technolog*" OR "off grid" OR "decentrali$ed" OR "community" OR "cooperative$"))
      OR "electrical grid$" OR "power grid$" OR "grid extension$" OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$" OR "smart grid$" OR "energy storage system$"
      OR
        (
          ("power station$" OR "power generation" OR "energy generation" OR "generator$")
          NEAR/5
              ("modern*" OR "clean" OR "sustainable" OR "renewable$" OR "decarboni*" OR "low carbon"
              OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower" OR "marine" OR "tidal" OR "wave energy"
              )
        )             
      )
  )
  AND  
    (
    "least developed countr*" OR "least developed nation$"
    OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
    OR "less developed countr*" OR "less developed nation$"
    OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
    OR "underserved countr*" OR "underserved nation$"
    OR "deprived countr*" OR "deprived nation$"
    OR "middle income countr*" OR "middle income nation$"
    OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
    OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
    OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
    OR
    "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    OR
    "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
    OR
    "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
    OR
    "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish" OR "turkey" OR "georgia"
    )
)      
```

### Works mentioning the SDG

This phrase finds research which mentions this SDG. We include this as we consider works mentioning the SDG as relevant, and want to ensure they are found. It includes terms for the goal, and excludes specialist terms that may use the `SDG` acronym.

```py
TS=
("SDG 7" OR "SDGs 7" OR "SDG7" OR "sustainable development goal$ 7"
OR ("sustainable development goal$" AND "goal 7")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 7")
    AND ("clean energy")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 7")
    NEAR/15 ("energy")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
```

## 4. Contributions

* v2019.12: Marta Lorenz, Caroline S. Armitage, Susanne Mikki

* v1.0.0: Caroline S. Armitage (Oct 2021-Oct 2022), Marta Lorenz (Oct 2021-Apr 2022)

* Internal review: Håkon Magne Bjerkan, Marta Lorenz (March 2022), Håkon Magne Bjerkan (minor review Oct 2022)

Specialist input: Shayan Shokrgozar (PhD candidate in energy transitions research, Jul 2022)

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
