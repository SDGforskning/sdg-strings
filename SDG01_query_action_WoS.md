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

Lists of least developed countries (LDCs) are from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) - countries were included if they appeared in the tables from 2016 to 2021 (i.e. were on these lists at any time between Nov 2015 and Dec 2020) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f22)</a>).

During editing of this string (2021), we have also consulted of queries from the <a id="Aurora">[Aurora Universities network (2020)](#f29)</a>

## 3. Targets

## Target 1.1

> **1.1 By 2030, eradicate extreme poverty for all people everywhere, currently measured as people living on less than $1.25 a day**
>
> 1.1.1 Proportion of the population living below the international poverty line by sex, age, employment status and geographic location (urban/rural)
>

This target is interpreted as to cover research about eradication of extreme poverty and reduce the number of people living below the international poverty line. 

`(("liv*" OR "surviv*" ) NEAR/5 "$1.25 "))` - taken out as adds irrelevant hits (picks up random numbers from abstracts) 

This query consists of 1 phrase.

Phrase 1: Covers research about eradicate extreme poverty (*515*)

*Action: decrease/eradicate*

*The basic structure is as follows: extreme/global poverty + action*

```Ceylon =
TS=
(
  ("extreme poverty" OR "severe poverty" OR "destitution" OR "global poverty" OR "international poverty")
   NEAR/10
    ("decreas*" OR "minimi*" OR "reduc*"
      OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
      OR "end" OR "ending" OR "eliminat*" OR "prevent*" OR "eradicat*"
      OR "lift out of" OR "lifting out of" OR "overcom*" OR "excap*" OR "mitigat*"
      )
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

This query consists of 1 phrase.(*20,899*)

*Action: decrease/eradicate*

*The basic structure is as follows: poverty/the poor + action*

```Ceylon =
TS=

(
  ("anti-poverty" 
    OR
    ("poverty"   OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
    OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))
     )
     
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

This target is interpreted as to cover research about about access to, coverage of and establishment/implementation of social protection systems, social services and social floors. Social floors encompasses a number of things such as essential health care, basic income security, child benefits, income support benefits, basic income, employment guarantees.

This query consists of 3 phrases.
All cover research about about access to, coverage of and establishment/implementation of social protection systems, social floors and social services. Some of the terms work well without groups of poeple (e.g welfare system), some need to be combined with "vulnerable people" ("unemployment benefit$") and some with poverty/"poor people"

Phrase 1: access/coverage/implementation + social protection systems (899)

Phrase 2: access/coverage/implementation + social protection systems/social floors + vulnerable groups (~~36)

Phrase 3: access/coverage/implementation + social protection systems/social services + poverty and the poor (~~184)

`welfare state` was concidered but excluded as it leads mostly to papers about early walfare states and the history of those.

##### Phrase 1: (*901*)

This phrase is about about access to, coverage of and establishment/implementation of social protection *systems*/welfare systems and similar concepts. As we talk about systems/services is does not need to be combined with groups of people.

*Action: access/coverage/implementation*

*The basic structure is as follows: action + social protection systems*

```Ceylon =
TS=
(
  ("implement*" OR "establish*" OR "plan" OR "plans" OR "planned" OR "planning" OR "build*" OR "architect" OR "develop" OR "development" OR "pathway$"
      OR "coverage" OR "covered" OR "covering" OR "access*" OR "barrier$" OR "obstacle$")
      
   NEAR/10
   
  ("welfare system$" OR "welfare service$" OR "social security system" OR "basic social service$" OR "social floor$")
)
  
 ```  


##### Phrase 2 (*113*):

This phrase is about about access to, coverage of and establishment/implementation of specific social social floors such as cash, sickness benefits for vulnerable groups 

*Action: access/coverage/implementation*

*The basic structure is as follows: action + social protection systems/social floors + vulnerable groups*

Vulnerable groups are based in the groups mentioned in the indicators

```Ceylon =
TS=
( 
  (
  "implement*" OR "establish*" OR "plan" OR "plans" OR "planned" OR "planning" OR "build*" OR "architect" OR "develop" OR "development" OR "pathway$"
      OR "coverage" OR "covered" OR "covering" OR "access*" OR "barrier$" OR "obstacle$"
      )
      
  NEAR/10
  
  (
  "basic income" OR "cash benefit"  OR "income security" 
  OR "unemployment benefit$" OR "sickness benefit$" OR "sick benefit"
  )
  AND
  (
  "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
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
      OR "pregnant" OR "pregnancy"
       OR "disability" OR "unemployed"
      OR "children" OR "child" OR "pregnant" OR "pregnancy" 
      OR  "maternity" OR "female" OR "women" OR "girls"
  )
)
```

##### Phrase 3 (*742*):

This phrase is about about access to, coverage of and establishment/implementation of social protection/social benefits and similar concepts. These terms need to be combined with groups of people/poverty/the poor. We did not include other "vulnerable groups as the terms are rather general; e.g. social services for children or mothers can be related to other things than poverty

*Action: access/coverage/implementation*

*The basic structure is as follows: action + social protection systems/social services + poverty and the poor*


```Ceylon =
TS=

(
  (
    ("implement*" OR "establish*" OR "propose*" OR "design*" 
      OR "plan" OR "plans" OR "planned" OR "planning" OR "build*" OR "architect" OR "develop" OR "development" OR"pathway$"
      OR "coverage" OR "covered" OR "covering" OR "access*" OR "barrier$" OR "obstacle$")
      
    NEAR/10 
  
    ("social protection$" OR "social benefits" OR "social security" OR "social service$" OR "health care benefit$")   
  ) 
AND
  ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
   )
  
)    
```  

## Target 1.4

> **1.4 By 2030, ensure that all men and women, in particular the poor and the vulnerable, have equal rights to economic resources, as well as access to basic services, ownership and control over land and other forms of property, inheritance, natural resources, appropriate new technology and financial services, including microfinance**
>
> 1.4.1 Proportion of population living in households with access to basic services
>
> 1.4.2 Proportion of total adult population with secure tenure rights to land, (a) with legally recognized documentation, and (b) who perceive their rights to land as secure, by sex and type of tenure

This target is interpreted to cover research about:

???? action term in the whole target needs to be disscused ???
*Action: ensure + access* OR should it be *Action: ensure OR access*

Phrase 1: ensure + access/right/opportunities (equal is considered to be implicit when those two combined) + economic resourses

Phrase 1b: remove + barriers + economic resourses

Phrase 2: ensure + access/implementation of basic services 

Phrase 3: ensure + acces/right to ownership of land and other property, inheritance



##### Phrase 1a:

*The basic structure is as follows: action (equal is considered to be implicit) + economic resourses  + "the poor"*


```Ceylon =
TS=

(
  (
     ("ensure" OR "establish*" OR "propose*" OR "implement*" OR "plan" OR "plans" OR "planned" OR "planning" OR "adopt*" OR "introduc*" OR "build*" OR                         "develop" OR "development" OR "attain*" OR  "achiev*" OR "improv*" OR "strengthen*" OR "increas*" 
            )
      NEAR/10
      ("access*" OR "equitab*" OR "equity" OR "equality" OR "ownership" OR "control"
      OR "equal" OR "share" OR "sharing" OR "affordab*" OR "right$" OR "empower*"
      "distribution" OR "redistribution" OR "equalit*" OR "inequalit*"
        OR "equitab*" OR "inequitab*" OR "benefit sharing"
      )
   )
  NEAR/5
  (
  (("economic*" OR "financial") NEAR/3 ("resourc*" OR "opportunit*" OR "asset*" OR "servic*"))
   "microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance" OR "micro credit" OR "micro-credit"
  OR "decent work" OR "paid work" OR "full employment" OR "labour market$"
  "income" OR "wealth" OR "money" OR "natural resourses" OR "banking")
  )
AND
 ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
      )
)

```
##### Phrase 1b:

*Action: overcome + barriers*

*The basic structure is as follows: action + economic resourses  + "the poor"*

```Ceylon =
TS=

(
  ("overcome" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*"
  )
  NEAR/10
  ("unequal" OR "unaffordab*" OR "barrier$" OR "obstacle$"
  )
  NEAR/5
  (
  (("economic*" OR "financial") NEAR/3 ("resources" OR "opportunities" OR "services"))
  
  OR "decent work" OR "paid work" OR "full employment" OR "labour market"
  "income" OR "wealth" OR "money" OR "natural resourses" OR "banking"
  )
  AND
 ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
      OR "the vulnerable" OR "vulnerable group$"
      OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
      )  
  
)


```

##### Phrase 2 (*1562*)

Phrase 2 covers access to basic services, as defined in the <a id="SDGMetrep">[UN Statistics Dvision SDG Indicators Metadata Repository, 2022](#f11)</a> 

*The basic structure is as follows: action + basic services* 

```Ceylon =
TS=

(
  (
    ("ensure" OR "establish*" OR "propose*" OR "implement*" OR "plan" OR "plans" OR "planned" OR "planning" OR "adopt*" OR "introduc*" OR "build*" OR                         "develop" OR "development" OR "attain*" OR  "achiev*" OR "improv*" OR "strengthen*" OR "increas*" 
    )
    NEAR/10
    ("access*" OR "equitab*" OR "equity" OR "equality"
      OR "equal" OR "share" OR "sharing" OR "affordab*" OR "right$" 
    )
    NEAR/10
    (
      ("basic" NEAR/3 "service$") 
      OR "clean water" OR ("drinking water" NEAR/3 ("service$" OR "source$" OR "facilit*" OR "basic")) 
      OR "sanitation service$" OR "sanitation facilit$" or "toilet facilit$" OR "basic sanitation" 
      OR "hygiene facilit*" OR "hygiene service*" OR "handwashing facility" OR "hand-washing facility" 
      OR "clean fuels" OR "clean technology" OR "basic electricity" OR "modern energy"   
      OR "basic mobility" OR "transport* system*" OR "transport* infrastructure*" OR "public transport*" 
      OR (("waste" OR "garbage" or "rubbish") NEAR/1 ("collection" OR "management") NEAR/1 ("service$" OR "facilit*")) 
      OR "health care" OR "health-care" OR "healthcare" OR "health service$" OR "medical service$" OR "medical care" 
      OR "basic education" OR "education services" OR "schooling services" OR "education system" OR "school system" 
      OR  "basic information services" OR "basic telecommunication services" OR "basic mobile services" 
    ) 
  )
  AND
  ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
    OR "the vulnerable" OR "vulnerable group$"
    OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*"
    OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
  ) 
)
```


##### Phrase 3 (3339):

*The basic structure is as follows: action + ownership of land, inheritance, property * 


```Ceylon =
TS=
(
  ("ensure" OR "establish*" OR "propose*" OR "implement*" OR "plan" OR "plans" OR "planned" OR "planning" OR "adopt*" OR "introduc*" OR "build*" OR                         "develop" OR "development" OR "attain*" OR  "achiev*" OR "improv*" OR "strengthen*" OR "increas*" 
  )
  NEAR/10
  ("access*" OR "equitab*" OR "equity" OR "equality"
    OR "equal" OR "share" OR "sharing" OR "affordab*" OR "right$" 
  )
  NEAR/10
  ("land holding$" OR "tenure right$" OR "land tenure"
  OR
  (("land" OR "lands" OR "farmland$" OR "inheritance" OR "property") NEAR/3 ("right*" OR "ownership"))
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

This target is interpreted to cover research about improving the resilience and reducing impacts of disasters for the poor and those in vulnerable situations. We consider "climate-related extreme events and other economic, social and environmental shocks and disasters" to cover all kinds of disasters. 

We have used the hazards listed in <a id="disasters">[Murray et al., (2021)](#f4)</a> to make a list of disasters based on their classification of hazards into hydrological/meteorological, geohazards, environmental, chemical, biological, technological, and societal.

The target is limited to "the poor and those in vulnerable situations". Disabled people, children, elderly people and pregnant women are included as groups in "vulnerable situations". We have also included least-developed countries, based on the assumption that these may be in a more vulnerable position when it comes to disasters. 

This query consists of 1 phrase. The basic structure is *action + disaster + vulnerable groups*.

```Ceylon =
TS=
(
  (
    (  
      (
        ("improv*" OR "increas*" OR "better" OR "enhanc*" OR "build" OR "strengthen*") 
        NEAR/5 ("resilien*" OR "coping" OR "cope" OR "protection")
      )
    OR  
      (
        ("mitigat*" OR "prevent*" OR "reduc*" OR "decreas*" OR "manag*") 
        NEAR/5 ("impact$" OR "vulnerab*" OR "exposure")
      )
    OR "policy" OR "policies" OR "Sendai Framework"
    OR "protect" OR "protecting" OR "safeguard*" OR "preparedness"  
    OR "safety net$" OR "social protection$" OR "social floor$" OR "social security"
    OR 
      (
        ("disaster$" OR "risk$")
        NEAR/3 ("plan*" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "medical response$" OR "program$" OR "programme$")
      )
    )
    NEAR/15
        ("disaster$" OR "catastrophe$"
        OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
        OR (("natural" OR "climat*") NEAR/3 ("hazard$" OR "catastrophe$" OR "disaster$"))
        OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
        OR "drought$" OR "flood*" 
        OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
        OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
        OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
        OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
        OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 
        OR (  
              ("anthropogenic" 
              OR "environmental" OR "deforestation" OR "desertification" OR "degredation" OR "pollution" OR "erosion"
              OR "chemical" OR "heavy metal$" OR "pesticide$"
              OR "biological" OR "disease" OR "zoonotic"
              OR "technological" OR "radioactive" OR "nuclear" OR "cyber" OR "industrial" OR "construction" OR "transportation"
              ) 
              NEAR/3 ("hazard$" OR "catastrophe$" OR "disaster$")
           ) 
        OR "outbreak$" OR "pandemic$" OR "epidemic$"
        OR "war" OR "wars" OR "armed conflict$"
        OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
        OR "financial crash*" OR "financial shock$" OR "financial disaster$" 
        OR "economic downturn$" OR "economic shock$" OR "economic disaster$"
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
    OR "least developed countr*" OR "least developed nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    )  
)
```

## Target 1.a


> **1.a Ensure significant mobilization of resources from a variety of sources, including through enhanced development cooperation, in order to provide adequate and predictable means for developing countries, in particular least developed countries, to implement programmes and policies to end poverty in all its dimensions.**
>
> 1.a.1 Total official development assistance grants from all donors that focus on poverty reduction as a share of the recipient country’s gross national income
>
> 1.a.2 Proportion of total government spending on essential services (education, health and social protection)

This target is interpreted to cover research about investment, increased resources, incl. development aid to implement programs and policies (to end) poverty in developing countries, in particular least developed countries. "to end" is considered to be implicit. 

This query consists of 1 phrase. (*111*)

*Action : improve invenstment, international aid*

*The basic structure is as follows:: action + programs + poverty*



```Ceylon =
TS=
( 
  (
    ("development aid" OR "development assistance" OR "development spending" OR "foreign aid" OR "international aid" OR "cooperation fund"
        OR "international cooperation" OR "international collaboration" 
        OR (
            ("government" OR "public" OR "international")
            NEAR/3 ("expenditure" OR "invest*" OR "financ*" OR "spending")
            NEAR/5 ("improv*" OR "enhanc*" OR "increas*" OR "strengthen" OR "attain" OR "achiev*"
            OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "promote"
                   )
           )         
    )
  NEAR/10
    ("programm" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "framework$" OR "planning" OR "service$" OR "agenc*"    )
  )
  AND
  ("anti-poverty" 
    OR
    ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
     OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))
    )
  )
  AND
  (
  "least developed countr*" OR "least developed nation$" 
  OR
  "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
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
  )
)
 
```  
 
 

## Target 1.b

> **1.b Create sound policy frameworks at the national, regional and international levels, based on pro-poor and gender-sensitive development strategies, to support accelerated investment in poverty eradication actions**
>
> 1.b.1 Pro-poor public social spending



## 4. Authorship and review

## 5. Footnotes

<a id="f29"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f4"></a> Murray, V. et al. (2021) Hazard Information Profiles: Supplement to UNDRR-ISC Hazard Definition & Classification Review: Technical Report: Geneva, Switzerland, United Nations Office for Disaster Risk Reduction; Paris, France, International Science Council. (https://council.science/publications/hazard-information-profiles/).[↩](#disasters)

<a id="f11"></a> UN Statistics Division SDG Indicators Metadata Repository, 2022 https://unstats.un.org/sdgs/metadata/files/Metadata-01-04-01.pdf [↩](#SDGTMetrep)

<b id="f2">2</b> UN (2017) *2017 HLPF Thematic Review of SDG 1: End Poverty in All its Forms Everywhere.*  https://sustainabledevelopment.un.org/content/documents/14379SDG1format-final_OD.pdf [↩](#HLPF2017)

<b id="f3">3</b> United Nations (2019) *World Economic Situation and Prospects (Statistical Annex)*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)
