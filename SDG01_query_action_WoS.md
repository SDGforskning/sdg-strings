# Search query for SDG 01 - No Poverty, Bergen action-approach.

***Current status**: This string is currently under active development to improve the phrases and structure. It is substantially changed from the original version it was based on (v2019.11). "Full query" not updated.* 

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 1
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes


## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 1</summary>

```

```

</details>

## 2. General notes

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/). 

Lists of least developed countries (LDCs)are from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) - countries were included if they appeared in the tables from 2016 to 2021 (i.e. were on these lists at any time between Nov 2015 and Dec 2020) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f22)</a>).

During editing of this string (2021), we have also consulted of queries from the <a id="Aurora">[Aurora Universities network (2020)](#f29)</a>

## 3. Targets

## Target 1.1

> **1.1 By 2030, eradicate extreme poverty for all people everywhere, currently measured as people living on less than $1.25 a day**
>
> 1.1.1 Proportion of the population living below the international poverty line by sex, age, employment status and geographic location (urban/rural)
>

This target is interpreted as to cover research about eradicate extreme poverty and reduce the number of people living below the international poverty line. 

`Decent work` was considered for inclusion as highlighted as the main route out of poverty in the High level political forum document <a id="HLPF2017">[UN (2017)](#f2)</a>. `Child labour` and `modern slavery` were included as elements of this. In this version these are now taken out, as they are not necessarily linked to poverty. However, articles linking these topics with poverty reduction can be expected to use the word poverty as well and therefore to be covered but the phrase below. If there is no link to poverty, then it is too indirect and should not be included here.

`(("liv*" OR "surviv*" ) NEAR/5 "$1.25 "))` - taken out as adds irrelevant hits (picks up random numbers from abstracts) and does not add results regarding poverty.

*For the topic approach terms such as: poverty line,  poverty indicator, ("poverty") NEAR/3 ("chronic* *" OR "extreme") should be included.*

This query consists of 2 phrases.

Phrase 1: Covers research about eradicate extreme poverty

*The basic structure is as follows: extreme/global poverty + action*

```Ceylon =
TS=
(
  ("extreme poverty" OR "severe poverty" OR "destitution" OR "global poverty" OR "international poverty")
   NEAR/5
    ("decreas*" OR "minimi*" OR "reduc*"
      OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
      OR "end" OR "ending" OR "eliminat*" OR "prevent*" OR "eradicat*"
      OR "lift out of" OR "lifting out of" OR "overcom*" OR "excap*" OR "mitigat*"
      )
  )  
```

Phrase 2 (WORK IN PROGRESS): Covers research about reducing the number of poeple livining below the international poverty line

Doesn't give any hits as stated here, might only work in the topic apporoach

```Ceylon =
TS=
(
  ("international poverty line" OR "$1.25 a day" OR "$1.9 a day" OR "$1.25 per day " OR "$1.9 per day")
    NEAR/5
        ("decreas*" OR "minimi*" OR "reduc*"
        OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
        OR "end" OR "ended" OR "ending" OR "eliminat*" OR "prevent*" OR "eradicat*"
        OR "lift out of" OR "lifting out of" OR "overcom*" OR "escap*" OR "mitigat*"
        )
  vunerable groups and people
    )

```



## Target 1.2

> **1.2 By 2030, reduce at least by half the proportion of men, women and children of all ages living in poverty in all its dimensions according to national definitions**
>
> 1.2.1 Proportion of population living below the national poverty line, by sex and age
>
> 1.2.2 Proportion of men, women and children of all ages living in poverty in all its dimensions according to national definitions

This target is interpreted as to cover research about poverty reduction in in all forms. 

`Decent work` was considered for inclusion as highlighted as the main route out of poverty in the High level political forum document <a id="HLPF2017">[UN (2017)](#f2)</a>. `Child labour` and `modern slavery` were included as elements of this. In this version these are now taken out, as they are not necessarily linked to poverty. However, articles linking these topics with poverty reduction can be expected to use the word poverty as well and therefore to be covered but the phrase below. If there is no link to poverty, then it is too indirect and should not be included here.

`(("liv*" OR "surviv*" ) NEAR/5 "$1.25 "))` - taken out as adds irrelevant hits (picks up random numbers from abstracts) and does not add results regarding poverty.

*For the topic approach terms such as: poverty line,  poverty indicator, ("poverty") NEAR/3 ("chronic* *" OR "extreme") should be included.*

This query consists of 1 phrase.

*The general structure is poverty/the poor + decrease*

```Ceylon =
TS=
(
  ("anti-poverty" OR
  "poverty" 
  OR "the poor" OR "the poorest"
  OR "rural poor" OR "urban poor" 
  OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))
  OR "working poor"
  NEAR/5
      ("decreas*" OR "minimi*" OR "reduc*"
      OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
      OR "end" OR "ended" OR "ending" OR "eliminat*" OR "prevent*" OR "eradicat*" OR "escape" OR "mitigate" OR "relief"
      OR "lift out of" OR "overcome"
      )
  )
)

```


## Target 1.3

> **1.3 Implement nationally appropriate social protection systems and measures for all, including floors, and by 2030 achieve substantial coverage of the poor and the vulnerable**
>
> 1.3.1 Proportion of population covered by social protection floors/systems, by sex, distinguishing children, unemployed persons, older persons, persons with disabilities, pregnant women, newborns, work-injury victims and the poor and the vulnerable
>

This target is interpreted as to cover research about about access to, coverage of and establishment/implementation of social protection systems, social services and social floors. 
`welfare state` was concidered but excluded as it leads mostly to historical papers about early walfare states.

This query consists of 2 phrases.

##### Phrase 1:

This pharse is about about access to, coverage of and establishment/implementation of social protection systems
```Ceylon =
TS=

(
  ("social protection$" OR "social service$"
  OR "welfare system$" OR "welfare service$" OR "social security system*" OR "social security service"
  OR "social floor$" OR "basic income" OR "cash benefits" OR "social benefits"
  )
  NEAR/10
      ("implement*" OR "establish*" OR "propose*" OR "design*" 
      OR "plan" OR "plans" OR "planned" OR "planning" OR "build*" OR "architect" OR "develop" OR "development" OR"pathway$" OR "path$" "route" "roadmap" 
       
      OR "coverage" OR "covered" OR "covering" OR "access*" OR "barrier$" OR "obstacle$"
        
    )

```

##### Phrase 2:

This phrase deals with social services with focus on certain groups. Combining these terms with specific groups avoids picking up publications using the terms basic services, social security and social welfare but not related to poverty (e.g. technological basic services or psychological wellbeing).

Variants of the second part of this phrase are used in several places in this SDG to link the topics with poverty, women or children etc. (as relevant to each target).

```Ceylon =
TS=
(
  ("social protection$" OR "social floor$" OR "social service$"
  OR "welfare system$" OR "welfare service$"
  OR "social welfare" OR "social security" 
  )
  NEAR/15
      ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "slum" OR "slums"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
      OR "workers" OR "women"
      OR
        (
          ("person$" OR "people" OR "adult$")
          NEAR/3
              ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")
        )
      OR "disability"
      OR
        (
          ("work" OR "workplace" OR "worker$" OR "occupational")
          NEAR/3
              ("injury" OR "injuries" OR "illness*")
        )
      OR "worker$ compensation"
      OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy"
      )
)
```


## Target 1.4

> **1.4 By 2030, ensure that all men and women, in particular the poor and the vulnerable, have equal rights to economic resources, as well as access to basic services, ownership and control over land and other forms of property, inheritance, natural resources, appropriate new technology and financial services, including microfinance**
>
> 1.4.1 Proportion of population living in households with access to basic services
>
> 1.4.2 Proportion of total adult population with secure tenure rights to land, (a) with legally recognized documentation, and (b) who perceive their rights to land as secure, by sex and type of tenure

This target is interpreted to cover research about access and implementation of basic services (phrase 1); financial services (phrase 3 -5 ) and acces and right to land 
(phrase 6 & )

Phrase 1 covers access to basic services, as defined in the <a id="SDGMetrep">[UN Statistics Dvision SDG Indicators Metadata Repository, 2022](#f11)</a> 

*We only include the general terms. This is rather boread but most of the basic services are covered in more detail in its spesific SDG (drinking water services, basic sanitation services, basic hygiene facilities in SDG 6; basic information services in SDG 9.c.1 (https://unstats.un.org/sdgs/metadata/files/Metadata-09-0C-01.pdf) ; clean fuels  in SDG 7, basic waste collection services SDG Indicator 11.6.1, basic mobility in SDG 11.2.1, basic education services SDG 4.1.1, basic health care in SDG 3.8.1.*

WORK IN PROGRESS DIFFERENT VERSJONS NEEDS FURTHER TESTING

##### Phrase 1. v1 basic:

Access to basic services

```Ceylon =
TS=

(
  ("basic services" OR "basic drinking water service$" OR "basic hygiene service$*" OR "basic sanitation service$*" OR "waste collection services" OR 
   OR "basic mobility" OR "basic health care service$" OR "basic education services" OR "basic information services" OR "clean fuels" )
   NEAR/10
  ("access*" OR "coverage" OR "barrier$" OR "obstacle$")
  NEAR/5
  ( "improv*" OR "strengthen*" OR "increas*" OR "enhanc*"
      OR "build" OR "building"=
      
      
)



```
##### Phrase 1. v2 utvidet:

Access and implementation to basic services

```Ceylon =
TS=

(
  ("basic services" 
   OR 
   "drinking water service$" or "drinking water source$" OR "source$ of drinking water" OR "drinking water facilit*" OR "basic drinking water$" 
   OR 
   "sanitation service$" OR "sanitation facilit$" or "toilet facilit$" 
   OR
   "hygiene facilit*" OR  "hygiene service*" OR "handwashing facility" OR "hand-washing facility"  
   OR 
   "clean fuels" OR "clean technology" OR "basic electricity" OR "modern energy"  
   OR 
   "basic mobility" OR "transport* system*" OR "transport* infrastructure*" OR "public transport*"
   OR 
   (("waste" OR "garbage" or "rubish") NEAR/1 ("collection" OR "managment") NEAR/1 ("service$" OR "facilit*")))
   OR
   "health care" OR "health-care" OR "healthcare" OR "health service$" OR "medical service$" OR "medical care"
   OR
   "education services" OR "schooling services" OR "education system" OR "school system"
   OR 
  
   (OR  "basic information services" OR "basic telecommunication services" OR "basic mobile services )
   NEAR/10
      ("implement*" OR "establish*"
      OR "coverage" OR "covered" OR "covering"
      OR "improv*" OR "strengthen*" OR "increas*" OR "enhanc*"
      OR "build" OR "building"
      OR "access*" OR "barrier$" OR "obstacle$")
   NEAR/5
     ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
      OR "the vulnerable" OR "vulnerable group$"
      )
)

Need to be change in case we exclude people bolk
??? (("LTE" OR "broadband" OR "3G" OR "narrowband" OR "2G" OR "mobile-cellular") NEAR/3 ("household" OR "housing" OR "home$" OR "living")

```

##### Phrase 3:

This phrase coveres acces to financial services; these phrases are so general that they must be combined with poverty/vulnerable groups even though the target concerns all people

```Ceylon =
TS=
(
  (
    ("income" OR "wealth" OR "money" OR "economic" OR "natural resource$" OR "banking")
    NEAR/10
      ("distribution" OR "redistribution" OR "equalit*" OR "inequalit*"
        OR "equitab*" OR "inequitab*" OR "benefit sharing"
        OR "right$" OR "ownership" OR "access" OR "control"
      )
  )
  AND
      ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
      OR "workers" OR "women"
      OR
        (
          ("person$" OR "people" OR "adult$")
          NEAR/3
              ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")
        )
      OR "disability"
      OR
        (
          ("work" OR "workplace" OR "worker$" OR "occupational")
          NEAR/3
              ("injury" OR "injuries" OR "illness*")
        )
      OR "worker$ compensation"
      OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy"
      OR "sustainable development"
      )
)
```

##### Phrase 4:

Microfinance: These topics are more specific so do not require combination. *added microcredit any reason why not?*

```Ceylon =
TS=
(
  "microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance" OR "micro credit" OR "micro-credit"
  OR "wage theft"
)
```

##### Phrase 5:

```Ceylon =
TS=
(
  "financial service$"
  NEAR/15
      ("right$" OR "access*" OR "availab*"
      OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "women"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
      OR "sustainable development"
      )
)
```

##### Phrase 6:
ownership of land

```Ceylon =
TS=
(
  ("land holding$" OR "tenure right$" OR "land tenure"
  OR
    (
      ("land" OR "lands" OR "farmland$" OR "inheritance" OR "property")
      NEAR/10
          ("right$" OR "ownership" )
    )
  )
  NEAR/15
      ("access" OR "benefit sharing"
      OR "equitab*" OR "inequitab*" OR "equal" OR "unequal" OR "equalit*" OR "inequalit*"
      OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "women"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
      OR "sustainable development"
      )
)
```

##### Phrase 7:
ownership of land part 2
```Ceylon =
TS=
(
  ("access" NEAR/5 ("land$" OR "farmland$")
  )
  NEAR/15
      ("equitab*" OR "inequitab*" OR "equal" OR "unequal" OR "equalit*" OR "inequalit*"
      OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "women"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
      OR "sustainable development"
      )
)
```

## Target 1.5

> **1.5 By 2030, build the resilience of the poor and those in vulnerable situations and reduce their exposure and vulnerability to climate-related extreme events and other economic, social and environmental shocks and disasters**
>
> 1.5.1 Number of deaths, missing persons and directly affected persons attributed to disasters per 100,000 population
>
> 1.5.2 Direct economic loss attributed to disasters in relation to global gross domestic product (GDP)
>
> 1.5.3 Number of countries that adopt and implement national disaster risk reduction strategies in line with the Sendai Framework for Disaster Risk Reduction 2015–2030
>
> 1.5.4 Proportion of local governments that adopt and implement local disaster risk reduction strategies in line with national disaster risk reduction strategies

This query consists of x phrases.

##### Phrase 1:

Inclusion of `vulnerab*` here will pick up publications discussing the livelihood vulnerability index.

Disabled people, children, elderly people and pregnant women included under "vulnerable". Least developed countries and small island developing states have been included due as their population is more likely to be poor and the countries likely to have lower institutional resilience. SIDS in particular may be exposed to environmental disasters. Lists of least developed countries (LDCs), small island developing states (SIDS) are from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) - countries were included if they appeared in the tables from 2016 to 2021 (i.e. were on these lists at any time between Nov 2015 and Dec 2020) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f22)</a>).

```Ceylon =
TS=
(
  (
    ("resilien*" OR "coping" OR "cope" OR "vulnerab*"
    OR "policy" OR "policies" OR "protect*" OR "preparedness"
    OR "safety net$" OR "social protection$" OR "social floor$" OR "social security"
    OR ("mitigat*" NEAR/5 "impact$")
    OR "Sendai Framework" 
    OR 
      (
        ("disaster$" OR "risk$")
        NEAR/3
            ("plan*" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "medical response$")
      )
    )
    NEAR/15
        (
           ("natural" OR "anthropogenic" OR "environmental" OR "climat$" OR "man-made") 
          NEAR/3 ("hazard*" OR "catastroph*" OR "disaster*" OR "shock$")
          )
          OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$"))
          OR "drought$" OR "flood*" OR "cold spells"
          OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" 
          OR "heatwave$" OR "heat-wave$" OR "wildfire*" OR "forest fire*" OR "wild-fire*" OR "forestfire*" OR
          OR "earthquake$" OR "volcanic activit*" OR "volcanic emission$" OR "volcanic eruption$"
          OR "landslide$" OR "rockslide$" OR "surface collapse$" OR "mud flow$"
          OR "land-slide$" OR "rock-slide$" OR "mud-flow$"
          OR "tipping point$"  
          OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
        
          OR "financial crash*" OR "economic downturn$" OR "socio-economic resilience"
         )
  )
  AND
      ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))
      OR
        (
          ("person$" OR "people" OR "adult$")
          NEAR/3
              ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")
        )
      OR "disability"
      OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy"
      OR
        (
          (("developing" OR "least developed") NEAR/3 ("state$" OR "nation$" OR "countr*"))
          OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
          OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands"       
        )
      )  
)
```

## Target 1.a/1.b

These targets are combined, as they cover similar topics.

> **1.a Ensure significant mobilization of resources from a variety of sources, including through enhanced development cooperation, in order to provide adequate and predictable means for developing countries, in particular least developed countries, to implement programmes and policies to end poverty in all its dimensions.**
>
> 1.a.1 Total official development assistance grants from all donors that focus on poverty reduction as a share of the recipient country’s gross national income
>
> 1.a.2 Proportion of total government spending on essential services (education, health and social protection)
>
> **1.b Create sound policy frameworks at the national, regional and international levels, based on pro-poor and gender-sensitive development strategies, to support accelerated investment in poverty eradication actions**
>
> 1.b.1 Pro-poor public social spending

This query consists of 1 phrase.

The policy aspect of this target should be captured by other parts of the query (e.g. policies for poverty eradication or improved social protection systems).

Disabled people, children, elderly people and pregnant women included under "vulnerable".
In this version we added government spending/development aid on  education and health services.

```Ceylon =
TS=
(
  ("development cooperation" OR "development aid" OR "official development assistance"
  OR "government spending"
  )		
  AND
      ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "women" 		
  	  OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))
      OR
        (
          ("person$" OR "people" OR "adult$")
          NEAR/3
              ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")
        )
      OR "disability"
  	  OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy"
  	  OR "social protection$" OR "social floor$" OR "social service$" OR "social security"
      OR "welfare system$" OR "social welfare" OR "welfare service$"
      OR "basic service$" OR "essential service$"
      OR "health care" OR "health-care" OR "healthcare" OR "health service$" OR "medical service$" OR "medical care"
      OR "education services" OR "schooling services" OR "education system" OR "school system"
      )
)
```

## General SDG

```Ceylon =
TS=
(
  "SDG$ 1" OR "SDG1" OR "SDG-1" OR "sustainable development goal$ 1"
    OR
    (
      ("sustainable development goal$" OR "SDG$" OR "goal 1")
      NEAR/15 "poverty"
    )
)
```

## 4. Authorship and review

## 5. Footnotes

<a id="f29"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f11"></a> UN Statistics Division SDG Indicators Metadata Repository, 2022 https://unstats.un.org/sdgs/metadata/files/Metadata-01-04-01.pdf [↩](#SDGTMetrep)

<b id="f2">2</b> UN (2017) *2017 HLPF Thematic Review of SDG 1: End Poverty in All its Forms Everywhere.*  https://sustainabledevelopment.un.org/content/documents/14379SDG1format-final_OD.pdf [↩](#HLPF2017)

<b id="f3">3</b> United Nations (2019) *World Economic Situation and Prospects (Statistical Annex)*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)
