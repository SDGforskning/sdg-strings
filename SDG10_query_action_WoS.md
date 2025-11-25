# Search query for SDG 10 - Reduced inequalities, Bergen action-approach.

Reduce inequality within and among countries 

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 10 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 10 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

## 3. Targets

### Target 10.1

> **10.1 By 2030, progressively achieve and sustain income growth of the bottom 40 per cent of the population at a rate higher than the national average**
>
> 10.1.1 Growth rates of household expenditure or income per capita among the bottom 40 per cent of the population and the total population

This target is interpreted to cover research about 

```py
TS=
 (
    ("bottom 40%" OR "bottom 40 percent" OR "bottom 40 per cent" OR "the poor" OR "the poorest" OR "low wage" OR
     "rural poor*" OR "urban poor*" OR "working poor*" OR "destitute$" OR "low income" OR "extreme* poor*" OR
     "extreme* poverty" OR "severe* poor*" OR "severe* poverty" OR "abject* poor*" OR "abject* poverty" OR
     "absolute* poor*" OR "absolute* poverty" OR "impoverished" OR "multidimension* poor*" OR "multidimension* poverty"
     OR "poor household$" OR "poor communit*"
    )
  AND
  (
    (
      ("foster*" OR "increas*" OR "promot*" OR "boost*" OR "enhanc*" OR "improv*" OR "better$" OR "attain*" OR "achiev*"
      OR "provid*" OR "ensur*" OR "guarantee*" OR "maintain*" OR "strengthen*" OR "develop$" OR "establish*" OR
      "sustain$" OR "sustaining" OR "standardi*" OR "regulari*" OR "consolidat*" OR "stabili*" OR "normali*" OR
      "uphold*" OR "stable" OR "fixed" OR "perpetual*" OR "lasting" OR "enduring" OR "facilitat*" OR "raise" OR "raising"
      OR "raised" OR "offer*" OR "heighten*"
      )
      NEAR/5
      ("income growth" OR "per capita consumption$" OR "per capita income$" OR "income per capita" OR
      "inclusive econom*" OR "welfare aggregate$" OR "shared prosperit*" OR "welfare distribution$" OR
      "inclusive growth" OR "income secur*" OR "income equalit*" OR "income stabilit*" OR "microfinanc*" OR
      "pro poor* growth" OR "propoor* growth" OR "pro poor* econom*" OR "propoor* econom*" OR "financial* selfrelian*"
      OR "financial* self relian*" OR "econom* equalit*" OR "econom* wellbeing" OR "econom* well being" OR
      "financ* equalit*" OR "financ* wellbeing" OR "financ* well being" OR "economic* selfrelian*" OR
      "economic* self relian*" OR "income convergenc*"
      )
    )
    OR
    (
      (
        ("reduc*" OR "lessen*" OR "decreas*" OR "narrow*" OR "mitigat*" OR "curb*" OR "alleviat*" OR "overcom*" OR
       "eradicat*" OR fight*
        )
      NEAR/5
        ("income inequalit*" OR "income insecur*" OR "income gap*" OR "income uncertain*" OR "income polari$ation" 
         OR "income instabilit*" OR "earning* instabilit*" OR "economic inequalit*" OR "income disparit*" OR "poverty" OR "gini index"
        )
      )
         OR ("anti poverty" OR "antipoverty" OR "out of poverty" OR "poverty lending")
    )
  )
)


```

### Target 10.2

> **10.2 By 2030, empower and promote the social, economic and political inclusion of all, irrespective of age, sex, disability, race, ethnicity, origin, religion or economic or other status**
>
> 10.2.1 Proportion of people living below 50 per cent of median income, by sex, age and persons with disabilities

This target is interpreted to cover research about 

```py

TS=
(
 (
  ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "foster*" OR "more efficient*" OR
    "more effectiv*" OR "higher$" OR "upgrad*" OR "scal* up" OR "build*" OR "expand*" OR "accelerat*" OR "heighten*"
    OR "advance$" OR "advancing" OR "develop$" OR "developing" OR "developed" OR "empower*" OR "promot*" OR "ensur*"
    OR "attain*" OR "achiev*" OR "encourag*" OR "facilitat*" OR "boost*" OR "offer*" OR "enabl*" OR "optimi$*" OR
    "establish*" OR "emphas*" OR "engag*" OR "extend*" OR "better$*"
   )

 NEAR/3

 ("social* inclu*" OR "economic* inclu*" OR "political* inclu*" OR "societal* inclu*" OR "financ* inclu*" OR "socio-economic* inclu*" OR "socioeconomic* inclu*" 
OR "social* integrat*" OR "economic* integrat*" OR "political* integrat*" OR "socio-economic* integrat*" OR "socioeconomic integrat*" OR "financ* integrat*"
OR "social* equal*" OR "economic* equal*" OR "political* equal*" OR "societal* equal*" OR"socio-economic* equal*" OR "socioeconomic* equal*"
OR "social* activit*" OR "societal* activit*" OR "financ* activit*" OR  "political* activit*" OR
   ("accessib*" NEAR/3
    ("economic*" OR "financ*" OR "labor" OR "labour" OR "political*" OR "legislat*" OR "decision-making" OR "societal*" OR "social*" OR "socio-economic*" OR "socioeconomic*"
OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "homeless"
OR   (( "poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
OR   (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
OR "disabled" OR "disabilities" OR "disability"
OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors" OR "unemployed" 
OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*" OR "non-binar*" OR "nonbinar*" OR "queer$" OR "intersex*" OR"gender$"
OR "living with HIV" OR "living with AIDS"
OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
OR "indigenous group$")
   )
  )
 )
 OR
 (
  (
    "decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR
    "declin*" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR
    "avoid*" OR "prevent*" OR "cure" OR "halt*" OR "resist*" OR "overcom*" OR "escap*" OR "relief*" OR
    "lift$ out of" OR "lifting out of" OR "diminish*" OR "abate$" OR "abating" OR "dismantl*" OR "impair*" OR  "nullif*" OR "hinder*" 
   )
 NEAR/3
   (
    "horizontal* inequal*" OR "horizontal* exclu*" OR "horizontal* marginal*" OR "horizontal vulnerab*" OR
    "social* exclu*" OR "economic* exclu*" OR "political* exclu*" OR "social* marginal*" OR "economic* marginal*"
    OR "political* marginal*" OR "societal exclu*" OR "societal marginal*" OR "intersecti* exclu*" OR
    "intersecti* vulnerab*" OR "intersecti* oppression*" OR "financ* exclu*" OR "social* inequal*" OR 
    "economic* inequal*" OR "political* inequal*" OR "societal* inequal*" OR "socio-economic* inequal*" OR
    "socioeconomic* inequal*" OR "socio-economic* marginal*" OR "socioeconomic* marginal*" OR "socio-economic* exclu*"
    OR "socioeconomic exclu*" OR "social* inactivit*" OR "economic* inactivit*" OR "financ* inactivit*" OR
    "political* inactivit*" OR "societal* inactivit*" OR "societal* isolat*" OR "social* isolat*" OR
    "economic* isolat*" OR "financ* isolat*" OR "political* isolat*"
   )
  )
 )

```

### Target 10.3

> **10.3 Ensure equal opportunity and reduce inequalities of outcome, including by eliminating discriminatory laws, policies and practices and promoting appropriate legislation, policies and action in this regard**
>
> 10.3.1 Proportion of population reporting having personally felt discriminated against or harassed within the previous 12 months on the basis of a ground of discrimination prohibited under international human rights law

This target is interpreted to cover research about 

```py
TS=

 ((((("ensur*" OR "secure$" OR "securing" OR "mak* sure" OR "mak* certain" OR "assure$" OR "assuring" OR "endors*"
  OR "strengthen*" OR "guarantee*" OR "improv*" OR "foster*" OR "enhance" OR "enhances" OR "enhanced" OR "enhancing")

NEAR/3
  ("equal" OR "equally" OR "equalit*" OR "inclusi*" OR "accessib*"
   )  
  )
 
OR

 (("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*"  
  OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" 
  OR "declin*" OR "abate$" OR "abating" OR "diminish*" OR "escap*" OR "relief*" OR "halt" OR "resist" OR "resists" OR "resisting"
  OR "lift$ out of" OR "lifting out of" OR "overcom*" OR "dismantl*" OR "impair*" OR "nullif*" OR "hinder*"
 )

NEAR/3

  ("discriminat*" OR "inequalit*" OR "unequal*" OR "harass*"
  OR "stigma$" OR "stigmati$ed" OR "stigmati$ation" OR "stigmati$ing"
  OR "ableis*" OR "inaccesib*"  OR "exclusion" OR "stereotyp*" OR "prejud*" 
  OR "barrier$" OR "obstacle$" OR "bias" OR "bias$ed" OR "biases" OR "intoleran*" OR "bigot*"
    )
   )
  )

AND

   ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "homeless"
   OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
   OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
   OR (("person$" OR "people$" OR "adult$" OR "woman" OR "women" OR "man" OR "men" ) NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
   OR "disabled" OR "disabilities" OR "disability"
   OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors" OR "unemployed" 
   OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*" OR "non-binar*" OR "nonbinar*" OR "queer$" OR "intersex*" OR "gender$"
   OR "living with HIV" OR "living with AIDS"
   OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
   OR "indigenous group$"
  )
 )

OR

 (("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*"  
  OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" 
  OR "declin*" OR "abate$" OR "abating" OR "diminish*" OR "escap*" OR "relief*" OR "halt*" OR "resist" OR "resists"
  OR "resisting" OR "lift$ out of" OR "lifting out of" OR "overcom*" OR "dismantl*" OR "impair*" OR "nullif*" OR
   "hinder*"
  )

NEAR/5

 ("racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*" OR "ageism" OR "agism" OR "hate speech" OR "religious discrimination"
  )
 )

OR

(("ensur*" OR "secure$" OR "securing" OR "mak* sure" OR "mak* certain" OR "assure$" OR "assuring" OR "endors*"
  OR "strengthen*" OR "guarantee*" OR "improv*" OR "foster*" OR "enhance" OR "enhances" OR "enhanced" OR "enhancing"
 )

NEAR/3

  ("egalitar*" OR "anti discriminat*" OR "antidiscriminat*" OR "non-discriminat*"
   )
  )
 )

```
Phrase 2

TS=

(((("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid*" OR
   "prevent*" OR "fight*" OR "combat*" OR "halt*" OR "resist" OR "resists" OR "resisting" OR "prohibit*" OR "dismantl*" OR
   "nullif*" OR "hinder*"
  )

NEAR

  (("discriminat*" OR "inequalit*" OR "harass*" OR "racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*"
    OR "stigma*" OR "ableis*" OR "inaccesib*" OR "unequal*" OR "exclusion" OR "bias" OR
    "bias$ed" OR "obstacle$" OR "barrier$"
   )

NEAR/5

   ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
    "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action*" OR "rule"
    OR "rules" OR "procedur*" OR "initiative*"
   )
  )
 )

OR

 (("promot*" OR "increas*" OR "strengthen*" OR "improv*" OR "enhance" OR "enhances" OR "enhanced" OR "enhancing" OR
   "better$" OR "more efficient*" OR "more effectiv*" OR "build*" OR "accelerat*" OR "advance$" OR "advancing" OR
   "develop$" OR "developing" OR "development" OR "encourag*" OR "facilitat*" OR "establish*" OR "propos*" OR
   "implement*" OR "adopt*" OR "introduc*" OR "boost*" OR "foster*" OR "reform$" OR "reforming" OR "reformed" OR
   "offer*" OR "heighten*"
  )

NEAR

  (("equal" OR "equally" OR "equalit*" OR "equal opportunit*" OR "equal-opportunit*" OR "anti discriminat*" OR
    "antidiscriminat*" OR "non-discriminat*" OR "inclusi*" OR "accessib*" OR "egalitar*" 
   )

NEAR/5

   ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR
    "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "practice$" OR "action*" OR "rule"
    OR "rules" OR "procedur*" OR "initiative*"
   )
  )
 )
)

AND

    ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "homeless"
   OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
   OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
   OR (("person$" OR "people$" OR "adult$" OR "woman" OR "women" OR "man" OR "men" ) NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
   OR "disabled" OR "disabilities" OR "disability"
   OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors" OR "unemployed" 
   OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*" OR "non-binar*" OR "nonbinar*" OR "queer$" OR "intersex*" OR "gender$"
   OR "living with HIV" OR "living with AIDS"
   OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
   OR "indigenous group$")
 )

```

### Target 10.4

> **10.4 Adopt policies, especially fiscal, wage and social protection policies, and progressively achieve greater equality**
>
> 10.4.1 Labour share of GDP
>
> 10.4.2 Redistributive impact of fiscal policy

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 10.5

> **10.5 Improve the regulation and monitoring of global financial markets and institutions and strengthen the implementation of such regulations**
>
> 10.5.1 Financial Soundness Indicators

This query consists of X phrases.

```py
TS=
(

)
```

### Target 10.6

> **10.6 Ensure enhanced representation and voice for developing countries in decision-making in global international economic and financial institutions in order to deliver more effective, credible, accountable and legitimate institutions**
>
> 10.6.1 Proportion of members and voting rights of developing countries in international organizations

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 10.7

> **10.7 Facilitate orderly, safe, regular and responsible migration and mobility of people, including through the implementation of planned and well-managed migration policies**
>
> 10.7.1 Recruitment cost borne by employee as a proportion of montlhy income earned in country of destination
>
> 10.7.2 Number of countries with migration policies that facilitate orderly, safe, regular and responsible migration and mobility of people
>
> 10.7.3 Number of people who died or disappeared in the process of migration towards an international destination
>
> 10.7.4 Proportion of the population who are refugees, by country of origin

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 10.a

> **10.a Implement the principle of special and differential treatment for developing countries, in particular least developed countries, in accordance with World Trade Organization agreements**
>
> 10.a.1 Proportion of tariff lines applied to imports from least developed countries and developing countries with zero-tariff

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 10.b

> **10.b Encourage official development assistance and financial flows, including foreign direct investment, to States where the need is greatest, in particular least developed countries, African countries, small island developing States and landlocked developing countries, in accordance with their national plans and programmes**
>
> 10.b.1 Total resource flows for development, by recipient and donor countries and type of flow (e.g. official development assistance, foreign direct investment and other flows)

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 10.c

> **10.c By 2030, reduce to less than 3 per cent the transaction costs of migrant remittances and eliminate remittance corridors with costs higher than 5 per cent**
>
> 10.c.1 Remittance costs as a proportion of the amount remitted
> 
This target is interpreted to cover research about 

```py
TS=
(

)
```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f1">UN DESA. (2025).</span> *Goals: Reduce inequality within and among countries*. https://sdgs.un.org/goals/goal10#targets_and_indicators [Accessed 2025.04.02]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/
