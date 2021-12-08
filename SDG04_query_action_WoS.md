# Search query for SDG 4 - Quality Education, Bergen action-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 4
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes


## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 4</summary>

```
  Test
```

</details>

## 2. General notes

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

## 3. Targets

## Target 4.1

> **4.1 By 2030, ensure that all girls and boys complete free, equitable and quality primary and secondary education leading to relevant and effective learning outcomes**
>
> 4.1.1 Proportion of children and young people (a) in grades 2/3; (b) at the end of primary; and (c) at the end of lower secondary achieving at least a minimum proficiency level in (i) reading and (ii) mathematics, by sex
>
> 4.1.2 Completion rate (primary education, lower secondary education, upper secondary education)

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 (
  ("education" OR "schooling" OR "tuition" OR "instruction") 
   NEAR/5
   ("primary" OR "secondary")
    NEAR/3
    ("free" OR "equitable" OR "quality")
  )
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ( 
  ("education" OR "schooling" OR "tuition" OR "instruction"
   ) 
    NEAR/3
    ("primary" OR "secondary"
    )
     NEAR/5
     ("complet*" OR "finish*" OR "graduat*"
     )
      NEAR/5
      ("ensur*" OR "increas*" OR "attain*")
  )
)
```
#### Phrase 3:

Phrase 3 doc

```Ceylon =
TS=
(
 (
  ("education" OR "schooling" OR "tuition" OR "instruction"
  )
   NEAR/5
   ("primary" OR "secondary")
   )
    NEAR/7
    (
    ("dropout" NEAR/5 ("reduc*" OR "decreas*" OR "minimi*" OR "lower*")
    )
  )  
)
```
#### Phrase 4:

Phrase 4 doc
Action terms left out, as they seem to drastically remove number of hits and eliminate relevant ones.
```Ceylon =
TS=
(
 (
   ("minim*")
   NEAR/5
   (
    ("proficienc*" OR "skill*") 
      NEAR/5 
      ("read*" OR "mathematic*")
   )
 ) 
)
```
## Target 4.2

> **4.2 By 2030, ensure that all girls and boys have access to quality early childhood development, care and pre‑primary education so that they are ready for primary education**
>
> 4.2.1 Proportion of children aged 24–59 months who are developmentally on track in health, learning and psychosocial well-being, by sex
>
> 4.2.2 Participation rate in organized learning (one year before the official primary entry age), by sex

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc
Adding action terms ("ensure*" OR "secure*")NEAR/3 at he beginning reduces hits from 29 to 1 (very relevant)
```Ceylon =
TS=
(
 (access*)
  NEAR/5
  (
   ("quality")
    NEAR/5
    (
     ("early childhood")
      NEAR/5
      ("development"OR "care")
     )
      OR
      ("pre-primary education")
   )
 )
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ( 
  ("children*" OR "boys and girls" OR "under-five")
 )  
   NEAR/5
   (
    ("developmental*")
     NEAR/5 ("on track" OR "health*" OR "sound")
   )
)
```
#### Phrase 3:
```Ceylon =
TS=
(
 ("ready" OR "readiness")
  NEAR
  ("primary education")
)
```
#### Phrase 4:
```Ceylon =
TS=
(

)
```

## Target 4.3

> **4.3 By 2030, ensure equal access for all women and men to affordable and quality technical, vocational and tertiary education, including university**
>
> 4.3.1 Participation rate of youth and adults in formal and non-formal education and training in the previous 12 months, by sex

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc
Adding "ensure" NEAR/3 to the phrase would reduce hits from 75 to 1...
Adding NEAR/3 ("education" OR "schooling" OR "tuition" OR "instruction") to the phrase would reduce hits from 75 to 6
Search terms "afford*" OR "quality" seem to make trouble - perhaps drop phrase 1 for phrase 2?

```Ceylon =
TS=
(
  ("access"
  )
  NEAR/5
  (
   ("afford*" OR "quality"
   )
    NEAR/5
    ("technic*" OR "vocation*" OR "tertiar*" OR "university"
    )
   )
  ) 
)
```
#### Phrase 2: 
Phrase 2 doc

```Ceylon =
TS=
(
 (
  ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "ensure*" OR "secure*")
  NEAR/3
   ("access")
  )
   NEAR/5
    (
    ("technic*" OR "vocation*" OR "tertiar*" OR "university")
     NEAR 3/
     ("education" OR "schooling" OR "tuition" OR "instruction" OR "training")
    ) 
 )
)
```
##### Phrase 3:

Phrase 3 doc
Adding action verbs radically decrease the number of hits
```Ceylon =
TS=
(
"participat*"
  NEAR/5
  ("formal" OR "non-formal"
  )
   NEAR/3
   ("education" OR "schooling" OR "tuition" OR "instruction" OR "training"
  )
)
```

## Target 4.4

> **4.4 By 2030, substantially increase the number of youth and adults who have relevant skills, including technical and vocational skills, for employment, decent jobs and entrepreneurship**
>
> 4.4.1 Proportion of youth and adults with information and communications technology (ICT) skills, by type of skill

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "build*" OR "develop*")
  NEAR/15
  (
   ("necessar*" OR "required" OR "relevant")
    NEAR/5
     ("skill*")
      NEAR/5
       ("employ*" OR "job*" OR "entrepreneur*")
   )
 )
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "build*" OR "develop*")
  NEAR/5
   (
    ("information and communication technology" OR "ICT") 
     NEAR/3 
     ("skill*")
    ) 
   )
```

## Target 4.5

> **4.5 By 2030, eliminate gender disparities in education and ensure equal access to all levels of education and vocational training for the vulnerable, including persons with disabilities, indigenous peoples and children in vulnerable situations**
>
> 4.5.1 Parity indices (female/male, rural/urban, bottom/top wealth quintile and others such as disability status, indigenous peoples and conflict-affected, as data become available) for all education indicators on this list that can be disaggregated

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc
In doubt about action terms here, as they reduce the number of hits (26>7)and seem to eliminate relevant articles.
```Ceylon =
TS=
(
 ("equit*" OR "equal*")
 NEAR/3
  ("gender")
   NEAR/5
   (("access")NEAR/5("education" OR "schooling" OR "tuition" OR "instruction"OR "training")
   )
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("vulnerab*")
 NEAR/5
 (
  ("access")
   NEAR/5
   ("education" OR "schooling" OR "tuition" OR "instruction"OR "training")
 )
)
```
##### Phrase 3:

Phrase 3 doc

```Ceylon =
TS=
(
 ("person$ with disabilit*"OR "disabl*")
  NEAR/5
  (
   ("access")
   NEAR/5
   ("education" OR "schooling" OR "tuition" OR "instruction"OR "training")
  )
)
```
##### Phrase 4:

Phrase 4 doc

```Ceylon =
TS=
(
 ("indigen*")
  NEAR/5
  (
   ("access")
    NEAR/5
    ("education" OR "schooling" OR "tuition" OR "instruction"OR "training")
  )
)
```

## Target 4.6

> **4.6 By 2030, ensure that all youth and a substantial proportion of adults, both men and women, achieve literacy and numeracy**
>
> 4.6.1 Proportion of population in a given age group achieving at least a fixed level of proficiency in functional (a) literacy and (b) numeracy skills, by sex

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
("achiev*" OR "reach*")
 NEAR 
 (
 ("basic" OR "fundament*" OR "functional")
  NEAR/5
   ("numera*" OR "litera*")
 )
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(

)
```

## Target 4.7

> **4.7 By 2030, ensure that all learners acquire the knowledge and skills needed to promote sustainable development, including, among others, through education for sustainable development and sustainable lifestyles, human rights, gender equality, promotion of a culture of peace and non-violence, global citizenship and appreciation of cultural diversity and of culture’s contribution to sustainable development**
>
> 4.7.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 ("educat* for")
  NEAR/5
  ("sustainab*" OR "sustainable development" OR "sustainable lifestyle")
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("educat* for")
  NEAR/5
  ("human right*" OR "gender equality" OR "peace*" OR "non-violen*" OR "global citizen*" OR "cultural divers*")
)
```
##### Phrase 3:

Phrase 3 doc

```Ceylon =
TS=
(
 ("educat*")
  NEAR
  (
   ("cultur*")
   NEAR("sustainab*")
  )
)
```
##### Phrase 4:

Phrase 4 doc

```Ceylon =
TS=
(
 (
  ("global citizen*" NEAR "education")
   NEAR
   ("educ* polic*"OR "currricul*" OR "teacher educ*" OR "student assess*")
 )
)
```
##### Phrase 5:

Phrase 5 doc

```Ceylon =
TS=
(
 (
  ("sustainable development*" NEAR "education")
   NEAR("educ* polic*"OR "currricul*" OR "teacher educ*" OR "student assess*")
 )
)
```

## Target 4.a

> **4.a Build and upgrade education facilities that are child, disability and gender sensitive and provide safe, non-violent, inclusive and effective learning environments for all**
>
> 4.a.1 Proportion of schools offering basic services, by type of service

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc
"Basic services" not included. Education or schooling is often counted as a basic service, but otherwise that term seems to refer to food, health etc. and be used in other, more general contexts than that of schools, education etc. 

```Ceylon =
TS=
(
 (
  ("education* facility" OR "education* facilities")
 )
  NEAR
  ("child*" OR "disab*" OR "gender"OR "all")
 ) 
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("school*"OR "educati*")
 NEAR/5
  (
   ("learning environment")
   NEAR 
   ("safe*" OR "non-violen*" OR "inclusive" OR "effective")
  )
)
```

## Target 4.b

> **4.b By 2020, substantially expand globally the number of scholarships available to developing countries, in particular least developed countries, small island developing States and African countries, for enrolment in higher education, including vocational training and information and communications technology, technical, engineering and scientific programmes, in developed countries and other developing countries**
>
> 4.b.1 Volume of official development assistance flows for scholarships by sector and type of study

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 ("scholarship*"
  NEAR/5
  ("availab*"OR "access" OR "obtain" OR "receiv*")
 )
  NEAR
  (
  "least developed countr*" OR "least developed nation$"OR "developing countr*" OR "developing nation$" OR "developing states" OR ("Africa*") 
  )
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("enrol*" OR "participat*" OR "partake")
  NEAR/5
  ("higher edu*" OR "vocational training" OR "information and communications technology" OR "ICT" OR ("educat* program*"))
   NEAR
   (
    ("other" OR "develop*") NEAR/3 ("countr*")
   )
)
```
##### Phrase 3:

Phrase 3 doc

```Ceylon =
TS=
(
 ("student mobility")
  NEAR
  ("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR "developing states" OR ("Africa*")
 )
)
```
##### Phrase 4:

Phrase 4 doc

```Ceylon =
TS=
(
 (
  ("international")
  NEAR
   ("scholarship*"OR "exchang*")
 )
  NEAR
   ("education")
    NEAR
    (
     ("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR "developing states" OR ("Africa*")
    )
)
```
##### Phrase 5:

Phrase 5 doc
"official development assistance" OR "oda" returns no relevant hits combined with "scholarship"", but combined with more general terms connected with education etc

```Ceylon =
TS=
(
 ("official development assistance" OR "oda")
  NEAR
  ("student*" OR "educat*"OR"school*")
)
```

## Target 4.c

> **4.c By 2030, substantially increase the supply of qualified teachers, including through international cooperation for teacher training in developing countries, especially least developed countries and small island developing States**
>
> 4.c.1 Proportion of teachers with the minimum required qualifications, by education level

This query consists of x phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 ("qualif* teacher$")
  NEAR
  ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "higher" OR "upgrad*" OR "scal* up")
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("teacher training"OR"teacher education")
   NEAR
   ("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR "developing states")
)
```
##### Phrase 3:

Phrase 3 doc

```Ceylon =
TS=
(
 ("teacher*")
  NEAR
  (
   ("minim*")NEAR("qualifi*")
  )
)
```
##### Phrase 4:

Phrase 4 doc

```Ceylon =
TS=
(
 ("teacher*")
  NEAR
  ("qualif*")
   NEAR
   (
    ("educat*")
     NEAR/3
     ("level")
   )
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
