# Search query for SDG 01 - No Poverty, Bergen action-approach.

**Current status**: This string undergoing editing after review. It is substantially changed from the original version it was based on (v2019.11).*

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

This target is interpreted as to cover research about eradication of extreme poverty and reduce the number of people living below the international poverty line. Here we consider relevance limited to research about absolute poverty, vs. target 1.2 which is about poverty generally.

This query consists of 1 phrase. The basic structure is *extreme/global poverty + action*.

`(("liv*" OR "surviv*" ) NEAR/5 "$1.25 "))` was taken out as adds irrelevant hits (picks up random numbers from abstracts). `international poverty` will cover international poverty line.

```Ceylon =
TS=
(
  ("extreme poverty" OR "severe poverty" OR "deep poverty" OR "abject poverty" OR "absolute poverty" OR "destitution"
  OR "global poverty" OR "international poverty"
  )
   NEAR/10
    ("decreas*" OR "minimi*" OR "reduc*" OR "mitigat*"
    OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
    OR "end" OR "ending" OR "eliminat*" OR "eradicat*" OR "prevent*"
    OR "lift out of" OR "lifting out of" OR "overcom*" OR "escap*" OR "relief"
    )
)  
```

## Target 1.2

> **1.2 By 2030, reduce at least by half the proportion of men, women and children of all ages living in poverty in all its dimensions according to national definitions**
>
> 1.2.1 Proportion of population living below the national poverty line, by sex and age
>
> 1.2.2 Proportion of men, women and children of all ages living in poverty in all its dimensions according to national definitions

This target is interpreted as to cover research about poverty reduction. Research about `decent work` was considered for inclusion, as this is highlighted as a route out of poverty in the High level political forum document <a id="HLPF2017">([UN 2017](#f2))</a>. However we have not included it - it is not necessarily linked to poverty, and articles linking this topic with poverty reduction can be expected to be covered by the phrase below.

This query consists of 1 phrase. The general structure is *poverty/the poor + action*

```Ceylon =
TS=
(
  "anti-poverty" OR "out of poverty"
  OR
  (
    ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
    OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))
    )
    NEAR/5
        ("decreas*" OR "minimi*" OR "reduc*" OR "mitigat*"
        OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
        OR "end" OR "ending" OR "eliminat*" OR "eradicat*" OR "prevent*"
        OR "lift out of" OR "lifting out of" OR "overcom*" OR "escap*" OR "relief"
        )
  )
)
```

## Target 1.3

> **1.3 Implement nationally appropriate social protection systems and measures for all, including floors, and by 2030 achieve substantial coverage of the poor and the vulnerable**
>
> 1.3.1 Proportion of population covered by social protection floors/systems, by sex, distinguishing children, unemployed persons, older persons, persons with disabilities, pregnant women, newborns, work-injury victims and the poor and the vulnerable

This target is interpreted as to cover research about establishment/implementation and improving access to/coverage of social protection systems, social services and social floors. Social floors encompass basic health care and basic income security for certain groups (children, elderly, unemployed or unable to work) <a id="socialfloors">([International Labour Organization n.d.](#f5))</a>. We consider research about social services included.

This query consists of 3 phrases. Some of the terms for services/systems work well without groups of people (phrase 1), but some need to be combined with "vulnerable people" or poverty (phrase 2).

##### Phrase 1

This phrase is about access to, coverage of and establishment/implementation of floors/ protection systems/welfare systems. As we talk about systems/services is does not need to be combined with groups of people.

The basic structure is *action + social protection systems*

`welfare state` was considered but excluded as it leads mostly to papers about early welfare states and the history of those.

```Ceylon =
TS=
(
  ("implement*" OR "establish*" OR "improv*" OR "enhanc*" OR "strengthen" OR "expand*"
  OR "plan" OR "plans" OR "planned" OR "planning" OR "build*" OR "architect"  OR "design*" OR "develop*" OR "pathway$"
  OR
    (
      ("increas*" OR "improv*" OR "enhanc*" OR "better" OR "attain" OR "achiev*" OR "provide" OR "providing" OR "provision"
      OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "advoca*"
      )
      NEAR/5 ("coverage" OR "covered" OR "covering" OR "access*")
    )
  OR
    (
      ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting"
      OR "alleviat*" OR "address*" OR "tackl*" OR "combat*" OR "fight*"
      OR "prevent*" OR "avoid*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
      OR "improv*" OR "manag*"
      )
      NEAR/5 ("barrier$" OR "obstacle$")
    )
  )
  NEAR/5
      ("welfare system$" OR "welfare service$" OR "social security system" OR "basic social service$" OR "social floor$"
      OR "social protection program*" OR "social safety net$" OR "safety net program*"
      )
)
```  


##### Phrase 2

This phrase is about specific social floors and systems, where the terms work better when combined with groups of people. The basic structure is *action + social protection systems/social floors + vulnerable groups*. The terms for *vulnerable groups* are based on the groups mentioned in the indicator.

```Ceylon =
TS=
(
  (
    ("implement*" OR "establish*" OR "improv*" OR "enhanc*" OR "strengthen" OR "expand*" OR "propose$"
    OR "plan" OR "plans" OR "planned" OR "planning" OR "build*" OR "architect" OR "design*" OR "develop*" OR "pathway$"
    OR
      (
        ("increas*" OR "improv*" OR "enhanc*" OR "better" OR "attain" OR "achiev*" OR "provide" OR "providing" OR "provision"
        OR "ensur*" OR "guarantee" OR "secure" OR "securing" OR "maintain*" OR "advoca*"
        )
        NEAR/5 ("coverage" OR "covered" OR "covering" OR "access*")
      )
    OR
      (
        ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting"
        OR "alleviat*" OR "address*" OR "tackl*" OR "combat*" OR "fight*"
        OR "prevent*" OR "avoid*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
        OR "improv*" OR "manag*"
        )
        NEAR/5 ("barrier$" OR "obstacle$")
      )
    )
    NEAR/5
          ("social protection$" OR "social benefits" OR "social security" OR "social service$"
          OR "basic income" OR "cash benefit$" OR "income security" OR "guaranteed income$" OR "living allowance"
          OR "unemployment benefit$" OR "unemployment compensation" OR "unemployment insurance" OR "unemployment allowance"
          OR "disability benefit$" OR "disability allowance" OR "disability pension$"
          OR "health care benefit$" OR "sickness benefit$" OR "sick benefit" OR "sick pay" OR "paid sick leave" OR "sickness allowance"
          OR "paid maternity leave" OR "paid maternal leave" OR "maternity pay" OR "maternity allowance" OR "parental benefit$" OR "paid parental leave"
          OR "child benefit$"
          OR "pension$ insurance" OR "pension plan$" OR "pension benefit$" OR "public pension$" OR "state pension$"
          )
  )
  AND
    ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor"
    OR "the vulnerable" OR "vulnerable group$" OR "marginali$ed groups" OR "marginali$ed group" OR "marginali$ed communities" OR "marginali$ed community"
    OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
    OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
    OR "disabled" OR "disabilities" OR "disability"
    OR "unemployed"
    OR "older people" OR "older adult$" OR "elderly" OR "elders" OR "retired people" OR "retired adults"
    OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*" OR "accident$"))
    OR "pregnant" OR "pregnancy" OR "children" OR "child" OR  "maternity" OR "female" OR "women" OR "girls"
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
* Ensuring access and rights to financial services ("financial inclusion"). We interpret this as money-based resources. For this we include research about access to forms of microfinance, digital finance and mobile money, plus other more traditional financial products/financial services. Includes credit, savings, payment services, fund transfers and insurance.
* Ensuring rights and access to economic resources and land/property/inheritance/natural resources (including rights for tenure, ownership and control, and security). We interpret "economic resources" to include mentioned elements such as land, natural resources and technology, but could also include human capital/labour (e.g. access to employment).
* Ensuring access to basic services

We based this interpretation of financial and economic resources on <a id="DESA">[Department of Economic and Social Affairs (2009)](#f7)</a> (p1), which states:
> Economic resources refer to the direct factors of production such as “immoveable” assets, including land, housing, common pool resources and infrastructure, as well as “moveable” assets, such as productive equipment, technology and livestock. Financial resources refer to money-based resources, including government expenditures, private financial flows and official development assistance, as well as income, credit, savings and remittances. [...] Labour is the primary resource available to the vast majority of people, particularly
those from low-income households [...]

Although the target states for "all men and women", we target the results to this SDG by combining the phrases also to an element about "the poor and the vulnerable". This includes terms for poverty, poor and marginalisation, as well as terms for developing countries and least developed countries (based on the assumption that the populations there, on a global scale, might be considered economically "poor"). We do this because a) some of the search terms are quite general (for example, appear in general economic research), and b) because other SDGs  refer to access to specific basic services (e.g. modern energy in SDG 7, essential healthcare in SDG 3); thus we assume that the most relevant research for this target should also consider poverty.

##### Phrase 1
This phrase covers ensuring access and rights to financial services. The basic structure is *action + access/rights + financial services*.

Sources of terms included <a id="DESA">[Department of Economic and Social Affairs (2009)](#f7)</a> and a digital financial inclusion report from the <a id="sgsa">[UNSGSA et al. (2018)](#f8)</a>.  

```Ceylon =
TS=
(
  (
    (
      (
        ("ensure" OR "establish*" OR "propose*" OR "implement*"
        OR "improv*" OR "increase" OR "increasing" OR "increased" OR "better"
        OR "adopt*" OR "introduc*" OR "build*" OR "plan" OR "planning" OR "plans"
        OR "develop" OR "development" OR "attain*" OR  "achiev*" OR "improv*" OR "strengthen*" OR "increas*"
        OR "program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "initiative$" OR "law$" OR "legislat*"
        )
        NEAR/5
            ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
            OR "ownership" OR "control" OR "right$"
            OR "affordab*" OR "empower*" OR "inclusion"
            )
      )
      OR
      (
        ("reduce" OR "reducing" OR "decreas*" OR "avoid*" OR "prevent*" OR "combat*"
        OR "overcome" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "dismantl*"
        )
        NEAR/5
            ("inaccessib*" OR "barrier$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*"
            OR "unaffordab*" OR "expensive" OR "exclusion" OR "unbanked"
            )      
      )
    )
    NEAR/15
          ("microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance" OR "microcredit" OR "micro-credit" OR "microloan$" OR "micro-loan$"
          OR "banks" OR "a bank" OR "banking" OR "bank account$"
          OR "digital finance" OR "mobile money" OR "electronic payments" OR "digital payment$" OR "fintech"
          OR "credit" OR "savings" OR "insurance" OR "payment service$" OR "transfer service$" OR "transfer funds"
          OR (("financial" OR "monetary") NEAR/1 ("resourc*" OR "opportunit*" OR "asset*" OR "servic*"))
          OR "financial inclusion"
          )
  )
  AND
      ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute"
      OR "the vulnerable" OR "vulnerable group$" OR "marginali*"
      OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless*"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
      OR "developing countr*" OR "developing nation$" OR "least developed countr*" OR "least developed nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      )
)
```

##### Phrase 2

This phrase covers ensuring access and rights to economic resources, natural resources, land, property and inheritance. The basic structure is *action + access/rights + resources*. "security" is used in phrases because otherwise there are many results about food security.

```Ceylon =
TS=
(
  (
    (
      (
        ("ensure" OR "establish*" OR "propose*" OR "implement*"
        OR "improv*" OR "increase" OR "increasing" OR "increased" OR "better"
        OR "adopt*" OR "introduc*" OR "build*" OR "plan" OR "planning" OR "plans"
        OR "develop" OR "attain*" OR  "achiev*" OR "improv*" OR "strengthen*" OR "increas*"
        OR "program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "initiative$" OR "law$" OR "legislat*"
        )
        NEAR/5
            ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
            OR "ownership" OR "control" OR "right$"
            OR "affordab*" OR "empower*" OR "inclusion" OR "sharing"
            OR "tenure security" OR "secure tenure" OR "income security" OR "secure livelihood$"
            )
      )
      OR
      (
        ("reduce" OR "reducing" OR "decreas*" OR "avoid*" OR "prevent*" OR "combat*"
        OR "overcome" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "dismantl*"
        )
        NEAR/5
            ("inaccessib*" OR "barrier$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*"
            OR "unaffordab*" OR "exclusion" OR "land grab*" OR "insecurity"
            )      
      )
    )
    NEAR/5
        ("economic resource$" OR "employment" OR "decent work" OR "paid work" OR "labour market$"
        OR "income" OR "livelihood$" OR "wealth" OR "inheritance"
        OR "land" OR "lands" OR "farmland$" OR "property" OR "natural resource$" OR "tenure"
        )
  )
  AND
      ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute"
      OR "the vulnerable" OR "vulnerable group$" OR "marginali*"
      OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless*"
      OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
      OR "marginali*"
      OR "developing countr*" OR "developing nation$" OR "least developed countr*" OR "least developed nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      )
)
```

##### Phrase 3

Phrase 3 covers access to basic services, as defined in the <a id="SDGMetrep">[UN Statistics Dvision SDG Indicators Metadata Repository, 2022](#f11)</a>

*The basic structure is as follows: action + basic services*

```Ceylon =
TS=

(
  (
    (
      ("ensure" OR "establish*" OR "propose*" OR "implement*"
      OR "improv*" OR "increase" OR "increasing" OR "increased" OR "better"
      OR "adopt*" OR "introduc*" OR "build*" OR "plan" OR "planning" OR "plans"
      OR "develop" OR "attain*" OR  "achiev*" OR "improv*" OR "strengthen*" OR "increas*"
      OR "program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "initiative$" OR "law$" OR "legislat*"
      )
      NEAR/5
          ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
          OR "ownership" OR "right$" OR "affordab*" OR "empower*" OR "inclusion"
          )
    )
    NEAR/10
        (("basic" NEAR/3 "service$")
        OR "clean water" OR ("drinking water" NEAR/3 ("service$" OR "source$" OR "facilit*" OR "basic"))
        OR "sanitation service$" OR "sanitation facilit$" or "toilet facilit$" OR "basic sanitation"
        OR "hygiene facilit*" OR "hygiene service*" OR "handwashing facility" OR "hand-washing facility"
        OR "clean fuels" OR "clean technology" OR "basic electricity" OR "modern energy"   
        OR "basic mobility" OR "transport* system*" OR "transport* infrastructure*" OR "public transport*"
        OR (("waste" OR "garbage" or "rubbish") NEAR/1 ("collection" OR "management") NEAR/1 ("service$" OR "facilit*"))
        OR "health care" OR "health-care" OR "healthcare" OR "health service$" OR "medical service$" OR "medical care"
        OR "basic education" OR "education services" OR "schooling services" OR "education system" OR "school system"
        OR "basic information services" OR "basic telecommunication services" OR "basic mobile services"
        )
  )
  AND
    ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute"
    OR "the vulnerable" OR "vulnerable group$" OR "marginali*"
    OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless*"
    OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
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

The target is limited to "the poor and those in vulnerable situations". Disabled people, children, elderly people and pregnant women are included as groups in "vulnerable situations", based on the indicator in 1.3. We have also included terms for least-developed countries and small-island developing states, based on the assumption that these may be in a more vulnerable position when it comes to disasters.

We have used the hazards listed in <a id="disasters">[Murray et al., (2021)](#f4)</a> to make a list of disasters based on their classification of hazards into hydrological/meteorological, geohazards, environmental, chemical, biological, technological, and societal.

This query consists of 1 phrase. The basic structure is *action + disaster + vulnerable groups*.

```Ceylon =
TS=
(
  (
    ("protect" OR "protecting" OR "safeguard*"  
    OR "safety net$" OR "social protection$" OR "social floor$" OR "social security"
    OR
      (
        ("improv*" OR "increas*" OR "better" OR "enhanc*" OR "build" OR "strengthen*"
        OR "develop" OR "developing" OR "implement"
        OR "build* capacity" OR "capacity building" OR "capacity development"
        )
        NEAR/5 ("coping" OR "cope" OR "adapt*" OR "resilien*" OR "mitigat*" OR "preparedness" OR "protection" OR "early warning")
      )
    OR  
      (
        ("mitigat*" OR "prevent*" OR "reduc*" OR "decreas*" OR "minimis*" OR "minimiz*" OR "manag*")
        NEAR/5 ("impact$" OR "vulnerab*" OR "exposure")
      )
    OR
      (
        ("establish*" OR "propos*" OR "implement*" OR "adopt*" OR "introduc*" OR "roadmap" OR "towards" OR "way to")
        NEAR/5
            (
              ("disaster$" OR "risk$")
              NEAR/3 ("plan" OR "plans" OR "planning" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "program$" OR "programme$" OR "policy" OR "policies" OR "medical response$")
            )
      )
    OR "Sendai Framework"
    )
    NEAR/15
        ("disaster$" OR "catastrophe$"
        OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
        OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
        OR "drought$" OR "flood*"
        OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
        OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
        OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
        OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
        OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
        OR (  
              ("anthropogenic" OR "natural" OR "climat*"
              OR "environmental" OR "deforestation" OR "desertification" OR "degredation" OR "pollution" OR "erosion"
              OR "chemical" OR "heavy metal$" OR "pesticide$"
              OR "biological" OR "disease" OR "zoonotic"
              OR "technological" OR "radioactive" OR "nuclear" OR "cyber" OR "industrial" OR "construction" OR "transportation"
              )
              NEAR/3 ("hazard$")
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
    OR "the vulnerable" OR "vulnerable group$" OR "marginali$ed groups" OR "marginali$ed group" OR "marginali$ed communities" OR "marginali$ed community"
    OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))
    OR (("person$" OR "people" OR "adult$") NEAR/3 ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly"))
    OR "disability"
    OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy"   
    OR "least developed countr*" OR "least developed nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
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

v2019.12: ML, CSA SRM
New version, first draft: ML (Feb 2022)
Internal review: HMB, CSA (March 2022)
New version, second draft: ML, CSA (May 2022)

## 5. Footnotes

<a id="f29"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f7"></a> Department of Economic and Social Affairs (2009) *2009 World Survey on the Role of Women in Development: Women’s Control over Economic Resources and Access to Financial Resources, including Microfinance*. United Nations. https://www.un.org/womenwatch/daw/public/WorldSurvey2009.pdf [↩](#DESA)

<a id="f5"></a> International Labour Organization (n.d.) Social protection floor. (https://www.ilo.org/secsoc/areas-of-work/policy-development-and-applied-research/social-protection-floor/lang--en/index.htm) [Accessed May 2022].[↩](#socialfloors)

<a id="f4"></a> Murray, V. et al. (2021) Hazard Information Profiles: Supplement to UNDRR-ISC Hazard Definition & Classification Review: Technical Report: Geneva, Switzerland, United Nations Office for Disaster Risk Reduction; Paris, France, International Science Council. (https://council.science/publications/hazard-information-profiles/).[↩](#disasters)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f8"></a> UNSGSA (Office of the United Nations Secretary-General’s Special Advocate for Inclusive Finance for Development, Her Majesty Queen Máxima of the Netherlands), the Better Than Cash Alliance, the United Nations Capital Development (UNCDF), and the World Bank. (2018). *Igniting SDG Progress through Digital Financial Inclusion*. https://www.betterthancash.org/explore-resources/igniting-sdg-progress-through-digital-financial-inclusion [accessed 30.04.2022] [↩](#sgsa)

<a id="f11"></a> UN Statistics Division SDG Indicators Metadata Repository, 2022 https://unstats.un.org/sdgs/metadata/files/Metadata-01-04-01.pdf [↩](#SDGTMetrep)

<a id="f2"></a> United Nations (2017) *2017 HLPF Thematic Review of SDG 1: End Poverty in All its Forms Everywhere.*  https://sustainabledevelopment.un.org/content/documents/14379SDG1format-final_OD.pdf [↩](#HLPF2017)

<a id="f3"></a> United Nations (2019) *World Economic Situation and Prospects (Statistical Annex)*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)
