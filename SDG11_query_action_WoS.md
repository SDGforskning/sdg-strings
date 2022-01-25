
# Search query for SDG 11 -Sustainable cities and communities, Bergen action-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 11
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes

## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 11</summary>

```
  Test
```

</details>

## 2. General notes

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

## 3. Targets

## Target 11.1

> **11.1 By 2030, ensure access for all to adequate, safe and affordable housing and basic services and upgrade slums**
>
> 11.1.1 Proportion of urban population living in slums, informal settlements or inadequate housing

This target interpreted to cover reasearch on

- Access to adequate, safe and affordable housing and basic services 

- Upgrading slums.  

Search terms are partly based on definitions of basic services, housing standards and slums found in SDG indicator metadata (https://unstats.un.org/sdgs/metadata/files/Metadata-11-01-01.pdf).  

This query consists of 3 phrases.

##### Phrase 1:

Acccess to housing

```Ceylon =
TS=( 
(("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up" OR "expand" OR "expansion*" OR "advance" OR "advancing" OR "develop" OR "developing") 
NEAR 
("adequate" OR "inadequate" OR "affordable" OR "safe" OR "unsafe" OR "safety" OR "secure" OR "insecure" OR "security") 
NEAR ("housing" OR "settlements" OR "living conditions")) 
) 
```
##### Phrase 2:

Access to basic services. Phrase differs from the one used in target 1.4, not sure which approach is best. 

```Ceylon =
TS=( 
("access") 
NEAR 
("basic services" OR "waste management" OR "sanitation" OR "water supply" OR "drinking water" OR "postal service*" OR "electricity service*" OR "public transportation")
) 

```
##### Phrase 3:

Upgrade slums

```Ceylon =
TS=( 
("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up" OR "expand" OR "expansion*" OR "advance" OR "advancing" OR "develop" OR "developing") 
NEAR 
("slum" OR "slums") 
) 
```

## Target 11.2

> **11.2 By 2030, provide access to safe, affordable, accessible and sustainable transport systems for all, improving road safety, notably by expanding public transport, with special attention to the needs of those in vulnerable situations, women, children, persons with disabilities and older persons**
>
> 11.2.1 Proportion of population that has convenient access to public transport, by sex, age and persons with disabilities

This target is interpreted to mean improving safe accessible public transport systems.


This query consists of 3 phrases.

##### Phrase 1:

The basic structure is improve + safe + Transport systems  

Challenge: The term "transport system" is used in several subjects as biology, chemistry and transport of oil. This is solved by
limiting the search with terms concerning land transport.


```Ceylon =
TS=((("transport system*" AND ("safe*" OR "secure*" OR "risk*" OR "sustainab*" OR "access*" OR "reliabl*" OR "affordable*"))
AND ("city" OR "cities" OR "urban" OR "municipalit*" OR "human settlement*" OR "town*" OR "neighborhood*" OR "village*"OR
"infrastructure*" OR vehicle* OR "road*" OR roads OR "railway*" OR  "waterway*" OR "travel*" OR "traffic*" OR bus OR "taxi*" 
OR "ferry" OR "ferries" OR  "vehicl*"  OR "vessel*" OR "train$" OR "underground*" OR "tube" OR "public transport*" OR "pedestrian*"
OR "maritim*"  OR "socio*" OR journey OR airport* OR cycl* )) AND ((improv* OR moderni* OR reduc* OR "increas*" OR "expand*"
OR "build*" OR "boost*" OR "raise*" OR "escalate*" OR "extend*" OR "develop*" OR "implement*" OR "establish*" OR "enhanc*")))
```
##### Phrase 2:

improve road safety   
The basic structure is safe+road+improve

```Ceylon =

TS=(((("safety" OR "safe*" OR "secure*" OR "hazardous*") NEAR/5 (("traffic*" OR "road*"  OR "highway$" OR "motorway$" OR "street*"
OR "cycling lanes" OR "walkway*" OR "walking path*" OR "sidewalk*" OR "speed limit*")) NEAR/5 (("improv*" OR "increase*" OR "enhance*"
OR  "reduce*" OR "develop*")))) NOT ("air traffic*" OR "food*"))
```

##### Phrase 3:

expand Public transport

The basic structure is expand+ "public transport"

```Ceylon =
TS=(("public transport") AND (improv* OR moderni* OR reduc* OR "increas*" OR "expand*" OR "build*" OR "boost*" OR "raise*" OR "escalate*" 
OR "extend*" OR "develop*" OR "implement*" OR "establish*" OR "enhanc*"))

TS=
```

## Target 11.3

> **11.3 By 2030, enhance inclusive and sustainable urbanization and capacity for participatory, integrated and sustainable human settlement planning and management in all countries**
>
> 11.3.1 Ratio of land consumption rate to population growth rate
>
> 11.3.2 Proportion of cities with a direct participation structure of civil society in urban planning and management that operate regularly and democratically

This target is interpreted to cover research about making urbanization processes more inclusive and sustainable, and improving human settlement planning and management with regards to participation, integration and sustainability. There are two key aspects: urbanization, and settlement planning and management.

This query consists of three phrases, combined as phrase 1 OR phrase 2 AND phrase 3

##### Phrase 1:

Urbanization

```Ceylon =
TS=
((improv* OR develop* OR enhanc*) NEAR(1) (urbani*))
)
```
##### Phrase 2:

Settlement planning

```Ceylon =
TS=
((settlement OR urban OR city or region*) NEAR(2) (plan*)
)
```
##### Phrase 3:

Aspects of improvement

```Ceylon =
TS=
((inclu* OR particip* OR sustainab* OR integr*)
)
```

## Target 11.4

> **11.4 Strengthen efforts to protect and safeguard the world’s cultural and natural heritage**
>
> 11.4.1 Total per capita expenditure on the preservation, protection and conservation of all cultural and natural heritage, by source of funding (public, private), type of heritage (cultural, natural) and level of government (national, regional, and local/municipal)

This query consists of 1 phrase.

##### Phrase 1:

Only cultural heritage included in first draft.

```Ceylon =
TS=
("cultur* heritage" OR "heritage object$" OR "heritage build*" OR "heritage site$")

AND ("maintain*" OR "conserv*" OR "preserv*" OR "sustain")

)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(

)
```

## Target 11.5

> **11.5 By 2030, significantly reduce the number of deaths and the number of people affected and substantially decrease the direct economic losses relative to global gross domestic product caused by disasters, including water-related disasters, with a focus on protecting the poor and people in vulnerable situations**
>
> 11.5.1 Number of deaths, missing persons and directly affected persons attributed to disasters per 100,000 population
>
> 11.5.2 Direct economic loss in relation to global GDP, damage to critical infrastructure and number of disruptions to basic services, attributed to disasters

This query consists of 4 phrases.

##### Phrase 1:

Copied and extended disaster search terms from SDG1. Included specific synonyms, delete some? 

```Ceylon =
TS=
(
((("natural" OR "anthropogenic" OR "environmental" OR "climat$" OR "man-made") NEAR/3 ("hazard*" OR "catastroph*" OR "disaster*" OR "shock$"))

OR 

("extreme$" NEAR/3 ("climat*" OR "weather" OR "meteorol*" OR "precipitation" OR "rain" OR "snow" OR "temperature$")) 

OR "climat* change$" OR "changing climate$" OR "global warming" OR "drought$" OR "flood*" OR "heatwave$" OR "heat-wave$" OR "cold spell$"
OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado$"
OR "storm$" OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "surface collapse$" OR "mud flow$" OR "tipping point$" or wildfire$ OR "forest fire$" or "avalanche$" or "tsunami$" or "tidal wave$" 

OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 

OR ("weather*" NEAR/3 "disaster*")) 

NEAR/15

(("death$" or "casualt*" or "mortalit*" or "missing") NEAR/15 ("prevent*" OR "reduc*" OR "decreas*" OR "minimi*" OR "lowering" OR "lowered" OR "limit" OR "limiting" OR "combat*" OR "tackl*" OR "eliminat*" OR "avoid*" OR "interven*"))

)
```
##### Phrase 2:

Opposite terminology of death, i.e. increase survival. Include mortality? Depends on scope (increase in certain diseases after tsunami).

```Ceylon =
TS=
(
((("natural" OR "anthropogenic" OR "environmental" OR "climat$" OR "man-made") NEAR/3 ("hazard*" OR "catastroph*" OR "disaster*" OR "shock$"))

OR 

("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$")) 

OR "climat* change$" OR "changing climate$" OR "global warming" OR "drought$" OR "flood*" OR "heatwave$" OR "heat-wave$" OR "cold spell$"
OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado$"
OR "storm$" OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "surface collapse$" OR "mud flow$" OR "tipping point$" or wildfire$ OR "forest fire$" or "avalanche$" or "tsunami$" or "tidal wave$" 

OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 

OR (weather* NEAR/3 disaster*)) 

NEAR/15 ((mortality NEAR/5 improv*) OR (surviv* NEAR/15 (improv* OR increas* or enhanc*))))

)
```
##### Phrase 3:


```Ceylon =
TS=
(
((("natural" OR "anthropogenic" OR "environmental" OR "climat$" OR "man-made") NEAR/3 ("hazard*" OR "catastroph*" OR "disaster*" OR "shock$"))

OR 

("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$")) 

OR "climat* change$" OR "changing climate$" OR "global warming" OR "drought$" OR "flood*" OR "heatwave$" OR "heat-wave$" OR "cold spell$"
OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado$"
OR "storm$" OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "surface collapse$" OR "mud flow$" OR "tipping point$" or wildfire$ OR "forest fire$" or "avalanche$" or "tsunami$" or "tidal wave$" 

OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 

OR (weather* NEAR/3 disaster*)) 

AND

(("gross global product$" or ((global or world) NEAR/3 ("domestic product$" or gdp$))) NEAR/30 (decrease* or declin* or reduc* or lower* or loss or losses))

)
```

##### Phrase 4:

Phrase 4 doc

```Ceylon =
TS=
(
((("natural" OR "anthropogenic" OR "environmental" OR "climat$" OR "man-made") NEAR/3 ("hazard*" OR "catastroph*" OR "disaster*" OR "shock$"))

OR

("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$"))

OR "climat* change$" OR "changing climate$" OR "global warming" OR "drought$" OR "flood*" OR "heatwave$" OR "heat-wave$" OR "cold spell$"
OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado$"
OR "storm$" OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "surface collapse$" OR "mud flow$" OR "tipping point$" or wildfire$ OR "forest fire$" or "avalanche$" or "tsunami$" or "tidal wave$"

OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))

OR (weather* NEAR/3 disaster*)) NEAR/30 ((("people" or "person*") NEAR/4 ("affect*" or "afflict*" or "distress*" or "disturb*" or "influenc*" or "upset*")) NEAR/15 ("prevent*" OR "reduc*" OR "decreas*" OR "minimi*" OR "lowering" OR "lowered" OR "limit" OR "limiting" OR "combat*" OR "tackl*" OR "eliminat*" OR "avoid*" OR "interven*"))
)

```
##### Phrase 5:
All included for indicator 11.5.2, too many synonyms for basic services? Verbs repeated due to search syntax and difference, might be edited?

```Ceylon =
TS=(
((("natural" OR "anthropogenic" OR "environmental" OR "climat$" OR "man-made") NEAR/3 ("hazard*" OR "catastroph*" OR "disaster*" OR "shock$"))

OR

("extreme$" NEAR/3 ("climat*" OR "weather" OR "meteorol*" OR "precipitation" OR "rain" OR "snow" OR "temperature$"))

OR "climat* change$" OR "changing climate$" OR "global warming" OR "drought$" OR "flood*" OR "heatwave$" OR "heat-wave$" OR "cold spell$"
OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado$"
OR "storm$" OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "surface collapse$" OR "mud flow$" OR "tipping point$" or wildfire$ OR "forest fire$" or "avalanche$" or "tsunami$" or "tidal wave$"

OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))

OR ("weather*" NEAR/3 "disaster*"))

AND

((((("gross global product$" or (("global" or "world") NEAR/3 ("domestic product$" or gdp$))) NEAR/15 ("decrease*" or "declin*" or "reduc*" or "lower*" or "loss" or "losses"))) OR (("critical infrastructure" OR "basic service$" OR "physical asset$" OR "social security" OR "social welfare" OR "drinking water service$" OR "sanitation service$" OR "hygiene service$" or "health service$" or "waste collection" OR "ICT" OR "education service$" OR "mobility" OR "transport*") NEAR/15 ("devast*" OR "destruct*" OR "destroy*" OR "damage*" OR "disrupt*" OR "broken"))) OR ((“Financial” or “economic” or “stock exchange”) NEAR/4 (“loss” or “losses” or “collapse*” or “crash*” or “decreas*” or “declin*” or “reduc*”)))
)

```

## Target 11.6

> **11.6 By 2030, reduce the adverse per capita environmental impact of cities, including by paying special attention to air quality and municipal and other waste management**
>
> 11.6.1 Proportion of municipal solid waste collected and managed in controlled facilities out of total municipal waste generated, by cities
>
> 11.6.2 Annual mean levels of fine particulate matter (e.g. PM2.5 and PM10) in cities (population weighted)
> 

This query consists of 3 phrases: "air quality" and 2 phrases for "waste management"

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=(((("city" OR "cities" OR "urban" OR "municipalit*" OR "public*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*") NEAR/3 ("smog*" OR "air pollution"  OR "suspended particles" )) NEAR/5 (("decreas*"OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR collect* OR manage* OR treat*))) 



OR (("city" OR "cities" OR "urban" OR "municipalit*" OR "public*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*") NEAR/3 ((improve OR enhance) NEAR/5 ("clean air" OR "air quality")))




```
##### Phrase 2:

Related to SDG 1.4.1, 6.3.1, 12.3.1.b, 12.5.1. Metadata from https://unstats.un.org/sdgs/metadata/files/Metadata-11-06-01.pdf. Split query to search for waste management or waste collection as its own query. Waste management and Waste (both with synonyms) are different concepts. A bit different action terms. 

```Ceylon =

TS=(("solid waste" OR "bulky waste" OR "household waste" OR "domestic waste" OR "commercial waste" OR "industrial waste" OR "MSW" OR ("end of life" NEAR "waste") OR ("eol" NEAR "waste") OR ("end of chain" NEAR "waste") OR ("eoc" NEAR "waste") OR "garbage" OR "rubbish") 

NEAR 

("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*"))
```

##### Phrase 3:

Related to SDG 1.4.1, 6.3.1, 12.3.1.b, 12.5.1. Metadata from https://unstats.un.org/sdgs/metadata/files/Metadata-11-06-01.pdf. Split query to search for waste management or waste collection as its own query. Waste management and Waste (both with synonyms) are different concepts. A bit different action terms. Combine phrase 2 and 3? Include specific waste management activities as recycling, incinerate etc?

```Ceylon =

TS=(((("waste" NEAR/3 "manag*") OR ("waste" NEAR/3 "collect*") OR ("garbage" NEAR/3 "manag*") OR ("garbage" NEAR/3 "collect*") OR ("rubbish" NEAR/3 "manag*") OR ("rubbish" NEAR/3 "collect*")) 

NEAR 

("environmental impact" OR "environmental assess*" OR "footprint*" OR "foot print*") 

NEAR 

("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "improv*" OR "ameliorat*" OR "better*")))

```


## Target 11.7

> **11.7 By 2030, provide universal access to safe, inclusive and accessible, green and public spaces, in particular for women and children, older persons and persons with disabilities**
>
> 11.7.1 Average share of the built-up area of cities that is open space for public use for all, by sex, age and persons with disabilities
>
> 11.7.2 Proportion of persons victim of physical or sexual harassment, by sex, age, disability status and place of occurrence, in the previous 12 months

This query consists of 2 phrases, combined with OR.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
("green space$" OR garden$ OR park$ OR "recreational area$" OR "public area$"

)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(safe OR inclus* OR access* OR unrestrict*
)
```

## Target 11.a

> **11.a Support positive economic, social and environmental links between urban, peri-urban and rural areas by strengthening national and regional development planning**
>
> 11.a.1 Number of countries that have national urban policies or regional development plans that (a) respond to population dynamics; (b) ensure balanced territorial development; and (c) increase local fiscal space

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(

)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(

)
```

## Target 11.b

> **11.b By 2020, substantially increase the number of cities and human settlements adopting and implementing integrated policies and plans towards inclusion, resource efficiency, mitigation and adaptation to climate change, resilience to disasters, and develop and implement, in line with the Sendai Framework for Disaster Risk Reduction 2015–2030, holistic disaster risk management at all levels**
>
> 11.b.1 Number of countries that adopt and implement national disaster risk reduction strategies in line with the Sendai Framework for Disaster Risk Reduction 2015–2030
>
> 11.b.2 Proportion of local governments that adopt and implement local disaster risk reduction strategies in line with national disaster risk reduction strategies

This query consists of x phrases.

##### Phrase 1:

Since name of Sendai includes disaster risk reduction it does not make sense to include as an action neither for national or local. Rather include synonyms for implementation? Few hits just for this simple search below. Add national or local to distinguish 11.b.1 and 11.b.2 perhaps, will not get many results.

```Ceylon =
TS=
(sendai framework" AND "implement*")

)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(

)
```

## Target 11.c

> **11.c Support least developed countries, including through financial and technical assistance, in building sustainable and resilient buildings utilizing local materials**
>
> No suitable replacement indicator was proposed. The global statistical community is encouraged to work to develop an indicator that could be proposed for the 2025 comprehensive review. See E/CN.3/2020/2, paragraph 23.

This query consists of 1 phrase.
https://unstats.un.org/sdgs/metadata/?Text=&Goal=11&Target=11.c - only target, no metadata.

Countries from SDG14. Truncated develop* and least develop*, made a difference.

##### Phrase 1:

Phrase 1 doc

```Ceylon =

TS=(((("develop*" OR "least develop*") NEAR/3 ("state*" OR "nation$" OR "countr*")) OR "developing world" OR LDC* OR SIDS OR "small island developing state*"OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands" ) 

NEAR/30 

(("local*" OR "native*") NEAR/5 "material*") 

NEAR/30 

("construct*" OR "build*"))

```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(

)
```

## General SDG

```Ceylon =
TS=
(

)
```

## 4. Authorship and review

## 5. Footnotes

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)


https://sdgs.un.org/sites/default/files/2021-10/Transportation%20Report%202021_FullReport_Digital.pdf

https://unstats.un.org/sdgs/metadata/?Text=&Goal=11&Target=11.6

https://unstats.un.org/sdgs/metadata/?Text=&Goal=&Target=11.2


