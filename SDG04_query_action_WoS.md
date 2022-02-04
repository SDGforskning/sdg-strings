# Search query for SDG 4 - Quality Education, Bergen action-approach.

Ensure inclusive and equitable quality education and promote lifelong learning opportunities for all.

***Current status**: This string is a first draft, under active development. It is currently being reviewed.*

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

This target is interpreted to cover research about

* Increasing completion of primary and secondary education			
* Access to quality primary and secondary education that is free and equitable			
* Achieving minimal proficiency in reading and mathematics			

This query consists of 4 phrases. Phrase 1 and 2 are concerned with increasing completion and reducing dropout rates respectively. Phrase 3 is about access to free and equitable primary and secondary education, and phrase 4 about achieving minimal proficiency in reading and mathematics.

##### Phrase 1:

In many medical and other studies that are not concerned with education as such, having completed a specific level of education is used as a parameter. To avoid including those, we have used many variants of the verb complete, but avoided "completed" and "complete*". The basic structure is education level + children + complete + increase.

```Ceylon =
TS=
(
 (
  ("primary school*" OR "elementary school*" OR "primary educat*" OR "middle school*" OR "secondary school*" OR "secondary education*" OR 
   (
    ("school" OR "education") 
   ) 
    NEAR/3
    ("boys" OR "girls" OR "kids" OR "children")
   )
  ) 
  NEAR/5
   (
    ("complete" OR ""completing" OR "completes" OR "completion" OR "school completion" OR "finish*" OR "graduate" OR "graduation" 
     NEAR/5
      ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better*" OR "ensure" OR "attain" OR "achiev*" )
   )
 )
)
```
##### Phrase 2:

In this phrase we reverse the concept of increasing school completion, and focus on reducing dropouts. The basic structure is education level + children + dropout + reduce.

```Ceylon =
(
 (
  ("primary school*" OR "elementary school*" OR "primary educat*" OR "middle school*" OR "secondary school*" OR "secondary education*" OR 
   (
    ("school" OR "education") 
    NEAR/3
    ("boys" OR "girls" OR "kids" OR "children")
   )
  ) 
  NEAR/5
   ("dropout*" OR "drop-out*" OR "drop out" OR "dropping out" OR "quit*" OR "early school-leaving")
   NEAR/5
   ("prevent*" OR "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "lower$" OR "improv*"
```
##### Phrase 3:

"Quality education" is a broad term, and the short name of SDG 4.  As specified by Unesco, https://en.unesco.org/themes/education/sdgs/material/04, "it specifically entails issues such as appropriate skills development, gender parity, provision of relevant school infrastructure, equipment, educational materials and resources, scholarships or teaching force." These are all adressed in the subsequent targets, therefore "quality education" is not elaborated further here. The basic structure is access + school + free/equitable/quality.

```Ceylon =
TS=
(
 (
  "access*" OR "enter*" OR "entr" OR "enroll*" OR "admission" OR "admit*"
   NEAR/3
  ("primary school*" OR "elementary school*" OR "primary educat*" OR "middle school*" OR "secondary school*" OR "primary education" OR "secondary education")
 )
  NEAR
  ("free" OR "equitab*" OR "quality")
)  
```
#### Phrase 4:

We considered including terms for primary and secondary education, but too many relevant hits were excluded, and we deem the delimitation unnecessary. The basic structure is increase + level of skills + reading and mathematics.
```Ceylon =
TS=
(
 ("increas*" OR "enhanc*" OR "ensure" OR "secure" OR "improv*" OR "achiev*")
  NEAR/5
   (
    ("basi*" OR "fundamental*" OR "minim*" OR "basic*" OR "core" OR "elementary")
     NEAR/10
     ("proficienc*" OR "skill*" OR "comprehen*")
      NEAR/5
       ("read*" OR "literac*" OR "mathematic*" OR "maths" OR "numera*")
    )
 )
```
## Target 4.2

> **4.2 By 2030, ensure that all girls and boys have access to quality early childhood development, care and pre‑primary education so that they are ready for primary education**
>
> 4.2.1 Proportion of children aged 24–59 months who are developmentally on track in health, learning and psychosocial well-being, by sex
>
> 4.2.2 Participation rate in organized learning (one year before the official primary entry age), by sex

This target is interpreted to cover research about

* Access to institutionalized, early childhood education (and care)
* Readiness for primary education

This query consists of 2 phrases.

##### Phrase 1:

The search term "care" is combined with "education" as using it alone would give too many hits that are only indirectly relevant to readiness for and participation in organized learning. The basic structure is access + early childhood education.

```Ceylon =
TS=
(
 ("access" OR "inclusion*" OR "inclusiv*" OR "discriminat*" OR "non-discriminat*" OR "equitab*" OR "non-equit*" OR "barrier*" OR "obstacle*" OR "hinder*")
 NEAR/5
  (
  (
   ("early childhood")
   NEAR/3
    ("care and education" OR "education")
   )
   OR
   ("pre-kindergarten*")
  )
)
```
##### Phrase 2:

The basic structure is school readiness OR children's development + school entry.

```Ceylon =
TS=
(
 (
  ("ready" OR "readiness" OR "prepared*
  NEAR
   ("primary education*" OR "primary school*" OR "elementary school*" OR "first grade" OR "1st grade*")
 )
  OR 
  "school readiness"
  OR
   (
    (
     ("children*" OR "under-five*" OR "early childhood")
    )
     NEAR/5 
     ("development*")
      NEAR 
      "school entry"
   )
)
```

## Target 4.3

> **4.3 By 2030, ensure equal access for all women and men to affordable and quality technical, vocational and tertiary education, including university**
>
> 4.3.1 Participation rate of youth and adults in formal and non-formal education and training in the previous 12 months, by sex

This target is interpreted to cover research about:
* Equal access for all to technical, vocational and tertiary education, including universities

We have interpreted the target widely, and included search terms to identify research on discrimination, barriers etc. that may prevent or hinder access.

This query consists of 3 phrases. The first two phrases contain many of the same terms, but they are combined differently to reduce noise, and to avoid including for instance a large quantity of articles about open access publishing and universities. In phrase 1, "access" is limited by the inclusion of action terms, and the condition that "university" must be near admission or enrollment. In phrase 2, "access" is limited by its combination with justice terms. This allows for a freer use of "university" and related terms. 

##### Phrase 1:

The basic structure is action + access + higher education

```Ceylon =
TS=
(
 (
  ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "ensure*" OR "secure" OR "initiative$" OR "intervention$")
  NEAR/5
  ("access*" OR "inclusion*" OR "inclusiv*" OR "discriminat*" OR "non-discriminat*" OR "equitab*" OR "non-equit*" OR "equal*" OR "barrier*" OR "obstacle*" OR "inequalit*" OR   "afford*")
  NEAR/15
  (
   (
    ("technic*" OR "vocation*" OR "tertiar*" OR "university")
    NEAR/3 
    ("education" OR "training" OR "school*" OR "learning") 
    OR 
    "higher education"
   ) 
    OR 
    (
     ("university" OR "universities") 
     NEAR/5 
     ("admission$" OR "enroll*")
    ) 
  )
 )
) 

```
##### Phrase 2:

The basic structure is justice terms + access + higher education

```Ceylon =
TS=
(
 (
  ("inclusion*" OR "inclusiv*" OR "discriminat*" OR "non-discriminat*" OR "equitab*" OR "non-equit*" OR "equal*" OR "barrier*" OR "obstacle*" OR "inequalit*") 
  NEAR/5 
  ("access")
 ) 
 NEAR/15
  (
   (
    ("technic*" OR "vocation*" OR "tertiar*") 
    NEAR/3 
    ("education" OR "training" OR "school*" OR "learning")
   ) 
  OR 
  "university" OR "universities" OR "higher education"
 ) 
)
```
##### Phrase 3:

```Ceylon =
TS= "inclusive higher education"
```
## Target 4.4

> **4.4 By 2030, substantially increase the number of youth and adults who have relevant skills, including technical and vocational skills, for employment, decent jobs and entrepreneurship**
>
> 4.4.1 Proportion of youth and adults with information and communications technology (ICT) skills, by type of skill

This target is interpreted to cover research about

* Reducing the number of youths and adults not in employment, education or training ("NEET")
* The impact of improved ICT skills on employability

This query consists of 2 phrases.

##### Phrase 1:

Phrase 1 doc
https://www.decentjobsforyouth.org/

```Ceylon =
TS=
(
("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*")
  NEAR/5
   ("NEET*" OR "not in employment, education or training") NOT ("protein" OR "nuclear") 
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "build*" OR "develop*" OR "relevan*")
  NEAR/5
  (
   ("information and communication technology" OR "ICT")
    NEAR/5
    ("skill*")
  )
   NEAR
   ("employ*" OR "job*" OR "entrepreneur*")
)
```

## Target 4.5

> **4.5 By 2030, eliminate gender disparities in education and ensure equal access to all levels of education and vocational training for the vulnerable, including persons with disabilities, indigenous peoples and children in vulnerable situations**
>
> 4.5.1 Parity indices (female/male, rural/urban, bottom/top wealth quintile and others such as disability status, indigenous peoples and conflict-affected, as data become available) for all education indicators on this list that can be disaggregated

This target is interpreted to cover research about
* Gender disparities in education
* Access to education for vulnerable persons
* Access to education for persons with disabilities
* Access to education for indigenous peoples

This query consists of 4 phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 (
  (
   ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "ensure*" OR "secure*" OR "reduc*" OR "remov*" OR "minimi*" OR "reduc*" OR     "limit*" OR "lower*" OR "fight*" OR "combat*"
   )	
   NEAR/3 
    (
     (
      "gender" OR "girl*" OR "woman*" OR "women*" OR "female*" OR "boy$" OR "man" OR "men" OR "male"
     )
     NEAR/5
      (
      "equit*" OR "non-equit*" OR "equalit*" OR "non-equalit*" OR "inequalit*" OR "balanc*" OR "unbalanc*" OR "disparit*" OR "discriminat*" OR "obstacle*" OR "barrier*" OR "hindrance*"
      )
     )
    ) 	
    NEAR/3	
     (
      (
       "school*" OR "educat*" OR "vocational training" OR "student*"
       )
     )
 )
)	
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS =
 (
  (
   (
    (
     "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "higher" OR "ensure*" OR "secure*" OR "stop*" OR "end*" OR "remov*" OR "eliminat*" OR "eradicat*" OR   "avoid" OR "prevent*" OR "combat*"
     )
     NEAR/5
     (
     "access" OR "admission*" OR "admit*" OR "inclusion*" OR "inclusiv*" OR "discriminat*" OR "non-discriminat*" OR "equitab*" OR "non-equit*" OR "barrier*" OR "obstacle*" OR "enter"
     )
   )
   NEAR/5
   (
   "school*" OR "educat*" OR "vocational training"
   )
 )
  NEAR
   vulnerab*
 )
)
```
##### Phrase 3:

Phrase 3 doc

```Ceylon =
TS=
(
 (
  (
   (
    "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "higher" OR "ensure*" OR "secure*" OR "stop*" OR "end*" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid" OR "prevent*" OR "combat*"
    )
    NEAR/5
    (
    "access" OR "admission*" OR "admit*" OR "inclusion*" OR "inclusiv*" OR "discriminat*" OR "non-discriminat*" OR "equitab*" OR "non-equit*" OR "barrier*" OR "obstacle*" OR "enter"
    )
   )
   NEAR/5
    (
     ("school*" OR "educat*" OR "vocational training")
    )
     NEAR
     (
     "person$ with disabilit*" OR "disab*"
     )
 )
)
```
##### Phrase 4:

Phrase 4 doc

```Ceylon =
TS =
(
 (
  (
   (
   "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "higher" OR "ensure*" OR "secure*" OR "stop*" OR "end*" OR "remov*" OR "eliminat*" OR "eradicat*" OR "avoid" OR "prevent*" OR "combat*"
   )
   NEAR/5
   (
    "access" OR "admission*" OR "admit*" OR "inclusion*" OR "inclusiv*" OR "discriminat*" OR "non-discriminat*" OR "equitab*" OR "non-equit*" OR "barrier*" OR "obstacle*" OR "enter"
    )
  )
  NEAR/5
   (
    (
    "school*" OR "educat*" OR "vocational training"
    )
   )
    NEAR
    indigen*
 )
)
```

## Target 4.6

> **4.6 By 2030, ensure that all youth and a substantial proportion of adults, both men and women, achieve literacy and numeracy**
>
> 4.6.1 Proportion of population in a given age group achieving at least a fixed level of proficiency in functional (a) literacy and (b) numeracy skills, by sex

This target is interpreted to cover research about
		
* Achieving minimal or functional proficiency in literacy and numeracy skills

This query consists of 2 phrases.

##### Phrase 1:

Phrase 1 doc
This is closely related to target 4.1, however, with the second phrase, more hits having to do with literacy and numeracy level but not with school/educational system as such are found 

```Ceylon =
TS=
(
 ("increas*" OR "enhanc*" OR "ensure" OR "secure" OR "improv*" OR "achiev*" OR "reach*")
  NEAR/5
   (
    ("basi*" OR "fundamental*" OR "minim*" OR "basic*" OR "core" OR "elementary" OR "functional") 
    NEAR
     ("proficienc*" OR "skill*" OR "comprehen*")
      NEAR/5
       ("read*" OR "literacy" OR "literate" OR "mathematic*" OR "maths" OR "numeracy" OR "numerate")
   )
)
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 ("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*")
  NEAR/3
   (" illitera*" OR "anal$abet*" OR "innumeracy*")
)
```

## Target 4.7

> **4.7 By 2030, ensure that all learners acquire the knowledge and skills needed to promote sustainable development, including, among others, through education for sustainable development and sustainable lifestyles, human rights, gender equality, promotion of a culture of peace and non-violence, global citizenship and appreciation of cultural diversity and of culture’s contribution to sustainable development**
>
> 4.7.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

This target is interpreted to cover research about
		
* Results and outcomes of education for sustainable development (ESD) and global citizenship (GCED) 
* Results and outcomes of education for human rights, gender equality, peace, non-violence and cultural diversity
* Education for sustainable development (ESD) and global citizenship (GCED) in education policies, curricula, teacher education and student assessments

This query consists of 3 phrases.

##### Phrase 1:

Phrase 1 doc
https://en.unesco.org/themes/education-sustainable-development
```Ceylon =
TS= 
 (
  (
   ("skill*" OR "knowledge" OR "competen*" OR "outcome*" OR "result*")
   NEAR
   ("ESD" OR "educat*")
    NEAR/5
    ("sustainabilit*" OR "sustainable development" OR "sustainable lifestyle")
   )
 )
```
##### Phrase 2:

Phrase 2 doc
The search phrase GCED for Global Citizenship Education, retrieved from https://en.unesco.org/themes/education-sustainable-development/toolbox/implementation#esd-impl-46 only returned irrelevant hits from medical, mathematical and chemical research
```Ceylon =
TS=
(
 (
  ("skill*" OR "knowledge" OR "competen*" OR "understand*" OR "outcome*" OR "result*")
   NEAR
   ("educat*")
    NEAR/5
    ("human right*" OR "gender equality" OR "peace*" OR "non-violen*" OR "global citizen*" OR "cultural divers*")
  )
 )
```
##### Phrase 3:

Phrase 3 doc

```Ceylon =
TS=
(
 (
  (
   (
    "sustainable development*" OR "sustainab*" OR "global citizen*"
    )
    NEAR 
    "educat*"
   )
    OR 
    (
    "ESD"
    )
  )
   NEAR
   (
   "educ* polic*" OR "currricul*" OR "teacher educ*" OR "student assess*"
  )
)
```

## Target 4.a

> **4.a Build and upgrade education facilities that are child, disability and gender sensitive and provide safe, non-violent, inclusive and effective learning environments for all**
>
> 4.a.1 Proportion of schools offering basic services, by type of service

This target is interpreted to cover research about
* Safe and inclusive learning environments
* Access to basic services such as electricity, internet, drinking water and sanitation facilities in schools

This query consists of 2 phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 ("school*" OR "education*")
  NEAR
   (
    ("learning environment")
    NEAR
    ("safe*" OR "secure*" OR "inclus*" OR "effectiv*")
   )
)
```
##### Phrase 2:

Phrase 2 doc
The definition of basic services in schools in retrieved from: http://tcg.uis.unesco.org/wp-content/uploads/sites/4/2019/08/sdg4-global-indicators-4.a.pdf

```Ceylon =
TS=
(
 (
  ("school*"OR "education* facility" OR "education* facilities")
  NEAR
   (
    ("access")
    NEAR/5
     ("electricit*" OR "internet*" OR "computer*" OR "adapted infrastructure*" OR "adapted material*" OR "drinking water*" OR "sanitation*" OR "handwash*")
   )
 )
)
```

## Target 4.b

> **4.b By 2020, substantially expand globally the number of scholarships available to developing countries, in particular least developed countries, small island developing States and African countries, for enrolment in higher education, including vocational training and information and communications technology, technical, engineering and scientific programmes, in developed countries and other developing countries**
>
> 4.b.1 Volume of official development assistance flows for scholarships by sector and type of study

This target is interpreted to cover research about
		
* Availabilty of scholarships to students from developing countries
* Official development assistance (ODA) concerning higher education and vocational training

This query consists of 2 phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS=
(
 ("scholarships*"
  NEAR
  ("students"
  )
 ) 
  NEAR
  (
  "least developed countr*" OR "least developed nation$"OR "developing countr*" OR "developing nation$" OR "developing states" OR "Africa*" 
  )
)
```
##### Phrase 2:

Phrase 2 doc
https://unstats.un.org/sdgs/metadata/files/Metadata-04-0b-01.pdf

```Ceylon =
TS = 
 (
  ("official development assistance" OR "ODA")
  NEAR 
   ("educat*" OR "training program*")
 )

```

## Target 4.c

> **4.c By 2030, substantially increase the supply of qualified teachers, including through international cooperation for teacher training in developing countries, especially least developed countries and small island developing States**
>
> 4.c.1 Proportion of teachers with the minimum required qualifications, by education level

This target is interpreted to include research about
* Improving teacher qualifications
* Teacher training in developing countries
* International cooperation for teacher training

This query consists of 3 phrases.

##### Phrase 1:

Phrase 1 doc

```Ceylon =
TS= 
 (
  ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up")
   NEAR
   (
    ("teach* qualification$" OR "teach* certific*")
   )
 )
```
##### Phrase 2:

Phrase 2 doc

```Ceylon =
TS=
(
 (
  ("teacher")
  NEAR
   ("education" OR "training")
  ) 
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
  ("level of qualification*" OR "qualification level")
)
```
##### Phrase 4:

Phrase 4 doc

```Ceylon =
TS=
(
 (
  ("teacher*")
   NEAR
   ("education*" OR "train*")
    NEAR
    ("international program*" OR "international cooperation*" OR "international partners*")
 )
)
```

## General SDG

```Ceylon =
TS=
(
"SDG$ 4" OR "SDG4" OR "SDG-4" OR "sustainable development goal$ 4"
    OR
    (
      ("sustainable development goal$" OR "SDG$" OR "goal 4")
      NEAR/15 "education"
    )
)
```

## 4. Authorship and review

## 5. Footnotes
<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)
