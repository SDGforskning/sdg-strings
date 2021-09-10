# Search query for SDG 01 - No Poverty, Bergen action-approach.

**Contents**

1. Full query in copy-pastable format (to be added at the end)
2. General notes about method for SDG 1
3. Documentation and string sections for each target
   * Target 1.1
   * Target 1.2
   * ...

## Full query

<details>
  <summary>Click to show the final copy-pastable full query for SDG 1</summary>

```
TS= ( ( "poverty" NEAR/5 ("decreas*" OR "minimi*" OR "reduc*" OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*" OR "end" OR "ended" OR "ending" OR "eliminat*" OR "prevent*" OR "eradicat*" OR "out of" OR "overcome") ) OR (("social protection$" OR "social floor$" OR "social service$" OR "welfare system$" OR "welfare service$") NEAR/10 ("implement*" OR "establish*" OR "coverage" OR "covered" OR "covering" OR "improv*" OR "strengthen*" OR "increas*" OR "enhanc*" OR "build" OR "building") ) OR ( ("social protection$" OR "social floor$" OR "social service$" OR "welfare system$" OR "welfare service$" OR "social welfare" OR "social security" OR "basic service$" OR "essential service$" ) NEAR/15 ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "the vulnerable" OR "vulnerable group$" OR "slum" OR "slums" OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*")) OR "workers" OR "women" OR (("person$" OR "people" OR "adult$") NEAR/3 ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")) OR "disability" OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*")) OR "worker$ compensation" OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy" ) ) OR ( (("income" OR "wealth" OR "money" OR "economic" OR "natural resource$" OR "banking") NEAR/10 ("distribution" OR "redistribution" OR "equalit*" OR "inequalit*" OR "right$" OR "ownership" OR "access" OR "control" OR "equitab*" OR "inequitab*" OR "benefit sharing") ) AND ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "the vulnerable" OR "vulnerable group$" OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*")) OR "workers" OR "women" OR (("person$" OR "people" OR "adult$") NEAR/3 ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")) OR "disability" OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*")) OR "worker$ compensation" OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy" OR "sustainable development" ) ) OR ("microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance" OR "wage theft") OR ( "financial service$" NEAR/15 ("right$" OR "access*" OR "availab*" OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "the vulnerable" OR "vulnerable group$" OR "women" OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*")) OR "sustainable development" ) ) OR ( ("land holding$" OR "tenure right$" OR "land tenure" OR (("land" OR "lands" OR "farmland$" OR "inheritance" OR "property") NEAR/10 ("right$" OR "ownership" )) ) NEAR/15 ("access" OR "benefit sharing" OR "equitab*" OR "inequitab*" OR "equal" OR "unequal" OR "equalit*" OR "inequalit*" OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "the vulnerable" OR "vulnerable group$" OR "women" OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*")) OR "sustainable development" ) ) OR ( ("access" NEAR/5 ("land$" OR "farmland$")) NEAR/15 ("equitab*" OR "inequitab*" OR "equal" OR "unequal" OR "equalit*" OR "inequalit*" OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "the vulnerable" OR "vulnerable group$" OR "women" OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "children" OR "communit*")) OR "sustainable development" ) ) OR ( ( ("resilien*" OR "coping" OR "cope" OR "vulnerab*" OR "policy" OR "policies" OR "protect*" OR "preparedness" OR "safety net$" OR "social protection$" OR "social floor$" OR "social security" OR (("disaster$" OR "risk$") NEAR/3 ("plan*" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "medical response$")) OR ("mitigat*" NEAR/5 "impact$") ) NEAR/15 (("extreme$" NEAR/2 ("climat*" OR "weather" OR "precipitation")) OR "climate change" OR "drought$" OR "flood*" OR "disaster$" OR "catastrophe$" OR "shock$" OR "financial crash*" OR "economic downturn$" OR "socio-economic resilience") ) AND ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "the vulnerable" OR "vulnerable group$" OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*")) OR (("person$" OR "people" OR "adult$") NEAR/3 ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")) OR "disability" OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy" OR ( (("developing" OR "least developed") NEAR/3 ("state$" OR "nation$" OR "countr*")) OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands" ) ) ) OR ( ("development cooperation" OR "development aid" OR "official development assistance" OR "government spending") AND ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "the vulnerable" OR "vulnerable group$" OR "women" OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*")) OR (("person$" OR "people" OR "adult$") NEAR/3 ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")) OR "disability" OR "babies" OR "infants" OR "newborn$" OR "children" OR "child" OR "pregnant" OR "pregnancy" OR "social protection$" OR "social floor$" OR "social service$" OR "social security" OR "welfare system$" OR "social welfare" OR "welfare service$" OR "basic service$" OR "essential service$") ) OR ("SDG-1" OR "SDG$ 1" OR "SDG1" OR "sustainable development goal$ 1" OR (("sustainable development goal$" OR "SDG$" OR "goal 1") NEAR/15 "poverty")) )
```

</details>

## General notes

Source of Targets and Indicators:
Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021]
<sup id="SDGT+Is">[1](#f1)</sup>

## Targets

## Target 1.1/1.2

These targets are combined, as they cover similar topics.

> **1.1 By 2030, eradicate extreme poverty for all people everywhere, currently measured as people living on less than $1.25 a day**
>
> 1.1.1 Proportion of the population living below the international poverty line by sex, age, employment status and geographic location (urban/rural)
>
> **1.2 By 2030, reduce at least by half the proportion of men, women and children of all ages living in poverty in all its dimensions according to national definitions**
>
> 1.2.1 Proportion of population living below the national poverty line, by sex and age
>
> 1.2.2 Proportion of men, women and children of all ages living in poverty in all its dimensions according to national definitions

This query consists of 1 phrase.

`Decent work` was considered for inclusion as highlighted as the main route out of poverty in the High level political forum document <sup id="HLPF2017">[2](#f2)</sup>. `Child labour` and `modern slavery` were included as elements of this. These are now taken out, as they are not necessarily linked to poverty. However, articles linking these with poverty reduction can be expected to use the word poverty also. If no link, then it is too indirect.

`(("liv*" OR "surviv*" ) NEAR/5 "$1.25 "))` - taken out as adds irrelevant hits (picks up random numbers from abstracts) and does not add results regarding poverty.

```Ceylon =
TS=
(
  "poverty"
  NEAR/5
      ("decreas*" OR "minimi*" OR "reduc*"
      OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
      OR "end" OR "ended" OR "ending" OR "eliminat*" OR "prevent*" OR "eradicat*"
      OR "out of" OR "overcome"
      )
)
```


## Target 1.3/1.4

These targets are combined, as they cover similar topics.

> **1.3 Implement nationally appropriate social protection systems and measures for all, including floors, and by 2030 achieve substantial coverage of the poor and the vulnerable**
>
> 1.3.1 Proportion of population covered by social protection floors/systems, by sex, distinguishing children, unemployed persons, older persons, persons with disabilities, pregnant women, newborns, work-injury victims and the poor and the vulnerable
>
> **1.4 By 2030, ensure that all men and women, in particular the poor and the vulnerable, have equal rights to economic resources, as well as access to basic services, ownership and control over land and other forms of property, inheritance, natural resources, appropriate new technology and financial services, including microfinance**
>
> 1.4.1 Proportion of population living in households with access to basic services
>
> 1.4.2 Proportion of total adult population with secure tenure rights to land, (a) with legally recognized documentation, and (b) who perceive their rights to land as secure, by sex and type of tenure

This query consists of 7 phrases.

##### Phrase 1:

Note more general terms such as "basic services" are not included here (as these have technology applications), but are combined in the next phrase in combination with poor and vulnerable groups.

```Ceylon =
TS=
(
  ("social protection$" OR "social floor$" OR "social service$"
  OR "welfare system$" OR "welfare service$"
  )
  NEAR/10
      ("implement*" OR "establish*"
      OR "coverage" OR "covered" OR "covering"
      OR "improv*" OR "strengthen*" OR "increas*" OR "enhanc*"
      OR "build" OR "building"
      )
)
```

##### Phrase 2:

Basic services and protections with focus on certain groups. Combining these terms with specific groups avoids picking up publications using the terms basic services, social security and social welfare but not related to poverty (e.g. technological basic services or psychological wellbeing).

Variants of the second part of this phrase are used in several places in this SDG to link the topics with poverty, women or children etc. (as relevant to each target).

```Ceylon =
TS=
(
  ("social protection$" OR "social floor$" OR "social service$"
  OR "welfare system$" OR "welfare service$"
  OR "social welfare" OR "social security" OR "basic service$" OR "essential service$"
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

##### Phrase 3:

These phrases are so general that they must be combined with poverty/vulnerable groups even though the target concerns all people

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

These topics are more specific so do not require combination

```Ceylon =
TS=
(
  "microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance"
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

Disabled people, children, elderly people and pregnant women included under "vulnerable". Least developed countries and small island developing states have been included due as their population is more likely to be poor and the countries likely to have lower institutional resilience. SIDS in particular may be exposed to environmental disasters. Lists of least developed countries, small island developing states and landlocked developing states are from the United Nations World Economic Situation and Prospects (tables F, H and I, pages 173-174)<sup id="UNLDCs">[3](#f3)</sup>.

```Ceylon =
TS=
(
  (
    ("resilien*" OR "coping" OR "cope" OR "vulnerab*"
    OR "policy" OR "policies" OR "protect*" OR "preparedness"
    OR "safety net$" OR "social protection$" OR "social floor$" OR "social security"
    OR ("mitigat*" NEAR/5 "impact$")
    OR
      (
        ("disaster$" OR "risk$")
        NEAR/3
            ("plan*" OR "strateg*" OR "reduc*" OR "relief" OR "manag*" OR "medical response$")
      )
    )
    NEAR/15
        (
          ("extreme$" NEAR/2 ("climat*" OR "weather" OR "precipitation"))
          OR "climate change" OR "drought$" OR "flood*"
          OR "disaster$" OR "catastrophe$" OR "shock$"
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

## Footnotes
<b id="f1">1</b> This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)".
(https://unstats.un.org/sdgs/indicators/indicators-list/) [↩](#SDGT+Is)

<b id="f2">2</b> UN (2017) 2017 HLPF Thematic Review of SDG 1: End Poverty in All its Forms Everywhere.  https://sustainabledevelopment.un.org/content/documents/14379SDG1format-final_OD.pdf [↩](#HLPF2017)

<b id="f3">3</b> United Nations (2019) World Economic Situation and Prospects (Statistical Annex). https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)
