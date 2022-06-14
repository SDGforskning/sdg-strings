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
* Ensuring access to quality primary and secondary education that is free and equitable			
* Achieving minimal proficiency in reading and mathematics			

This query consists of 4 phrases. Phrase 1 and 2 are concerned with increasing completion and reducing dropout rates respectively. Phrase 3 is about ensuring access to free and equitable primary and secondary education, and phrase 4 about achieving minimal proficiency in reading and mathematics.

##### Phrase 1:

In many medical and other studies that are not concerned with education as such, having completed a specific level of education is used as a parameter. To reduce the number of such studies, we have used many variants of the verb complete, but avoided "completed" and "complete*". The basic structure is education level + children + complete + increase.

```Ceylon =
TS=
(
 (
  ("primary school*" OR "elementary school*" OR "primary educat*" OR "middle school*" OR "secondary school*" OR "secondary education*" OR 
   (
    ("school" OR "education") 
   ) 
    NEAR/3
    ("boys" OR "girls" OR "kids" OR "child*")
   )
  ) 
  NEAR/5
   (
    ("complete" OR "completing" OR "completes" OR "completion" OR "school completion" OR "finish*" OR "graduate" OR "graduation" 
     NEAR/5
      ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better*" OR "ensure" OR "attain" OR "achiev*" )
   )
 )
)
```
##### Phrase 2:

In this phrase we reverse the concept of increasing school completion, and focus on reducing dropouts. The basic structure is education level + children + dropout + reduce.

```Ceylon =
TS=
(
 (
  ("primary school*" OR "elementary school*" OR "primary educat*" OR "middle school*" OR "secondary school*" OR "secondary education*" OR 
   (
    ("school" OR "education") 
    NEAR/3
    ("boys" OR "girls" OR "kids" OR "child*")
   )
  ) 
  NEAR/5
   ("dropout*" OR "drop-out*" OR "drop out" OR "dropping out" OR "quit*" OR "early school-leaving")
   NEAR/5
   ("prevent*" OR "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "lower$" OR "improv*")
 )
)
```
##### Phrase 3:

"Quality education" is a broad term, and the short name of SDG 4.  As specified by Unesco, https://en.unesco.org/themes/education/sdgs/material/04, "it specifically entails issues such as appropriate skills development, gender parity, provision of relevant school infrastructure, equipment, educational materials and resources, scholarships or teaching force." These are all adressed in the subsequent targets, therefore "quality education" is not elaborated further here. The basic structure is increase + access + school + free/equitable/quality.

```Ceylon =
TS=
(
 (
  (
   ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "scal* up" OR "build*" OR "expand"  OR "accelerat*" OR "ensure" OR  "attain*" OR "achiev*" )  
   NEAR
   ("access*" OR "enter*" OR "entr" OR "enroll*" OR "admission" OR "admit*"))
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

* Ensuring access to institutionalized, early childhood education (and care)
* Readiness for primary education

This query consists of 2 phrases.

##### Phrase 1:

The search term "care" is not used alone as it would give too many hits that are only indirectly relevant to readiness for and participation in organized learning. Variants of daycare were considered, but returned too many hits not considered relevant to the target. The basic structure is improve access / remove obstacles + early childhood education and care. Some agricultural terms which occur in combinations with "nurser*" had to be excluded with NOT.

```Ceylon =
TS=
(
 ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "overcome" OR  "ensure" OR "attain*" OR "achiev*" OR "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limiting" OR "limited" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*") 
 NEAR/5 
  ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*")
  NEAR/5
  (
   (
    ("early childhood")
    NEAR/3
    ("education")
   )
   OR
   ("early childhood care" OR "kindergarten" OR "pre-kindergarten*" OR "nurser*" OR "pre-primary*" OR "pre school*" OR "preschool*" OR "under five$")
 )
  NOT 
  ("pig*" OR "plant*" OR "fish*") 
)
```
##### Phrase 2:

The basic structure is school readiness OR children's development + school entry.

```Ceylon =
TS=
(
 (
  ("ready" OR "readiness" OR "prepared*")
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

We have interpreted the target widely, and included search terms to identify research on discrimination, barriers etc. that may prevent or hinder access. We have also included post-secondary education, which is in Unesco's International Standard Classification of Education (ISCED) http://uis.unesco.org/en/topic/international-standard-classification-education-isced a level between upper secondary and tertiary education, which does not necessarily give access to tertiary education, and is often practically or vocationally, as opposed to theoretially or generally, oriented. 

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
    ("technic*" OR "vocation*" OR "tertiar*" OR "university" OR "postsecondary" OR "post secondary")
    NEAR/3 
    ("education" OR "training" OR "school*" OR "learning") 
    OR 
    "higher education"
   ) 
    OR 
    (
     ("university" OR "universities" OR "college$") 
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
    ("technic*" OR "vocation*" OR "postsecondary" OR "post secondary" OR "tertiar*") 
    NEAR/3 
    ("education" OR "training" OR "school*" OR "learning")
   ) 
  OR 
  "university" OR "universities" OR "higher education" OR "college$"
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

* Increasing the number of youths and adults who have relevant skills for employment and entrepreneurship
* Improvement of ICT skills and employability

This query consists of 4 phrases. The first two cover skills at an overriding level, the third core skills as defined by ILO, and the fourth ICT skills. In order to limit the search to research concerning opportunities for employment and avoid articles having to do with employees and employers and their (needs for) development in jobs and workplaces, only "employability" and "employment" are used alongside jobs and entrepreneurship. The term "work" is not included as it gives too much noise. 

##### Phrase 1:

The basic structure is action + skills + employability/entrepreneurship

```Ceylon =
TS=
(
 ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "build*" OR "develop*")
  NEAR/5
   ("skill$" OR "abilit*" OR "competenc*" OR "literac*") 
    NEAR/5
    ("employability*" OR "employment" OR "decent job$" OR "entrepreneurship$")
 )
```
##### Phrase 2:

This phrase finds research talking about skills, competencies etc. in relation to reducing unemployment. The basic structure is action + unemployment + skills 

```Ceylon =
TS=
(
 ("reduc*" OR "decreas*" OR "lower*"  OR "prevent*" OR "minimi*" OR "limit*" OR "eliminat*")
  NEAR/5
  ("unemploy*" OR "underemploy*") 
   NEAR/5 
   ("skill$" OR "abilit*" OR "competenc*" OR "literac*" OR "literate") 
 )
 ```
##### Phrase 3:

Terms are from ILO: https://www.ilo.org/wcmsp5/groups/public/@ed_emp/@ifp_skills/documents/publication/wcms_213452.pdf. Employment is omitted as a search term here, as it leads to too much noise from articles concerned with the use (="employment") of the skills. The basic structure is core and transferable skills + employability

```Ceylon =
TS= 
(
 (
  ("learn and adapt") OR (("read*" OR "writ*" OR "comput*")) OR (("listen*" OR "communicat*") NEAR/3 "effective*") OR ("think creatively" OR "creative thinking") OR ("solve problem$" OR "problem-solv*") OR (("interact*") NEAR ("co-work*")) OR (("work*")NEAR/3 ("team*" OR "group*")) OR ("basic technolog*") OR (("lead*") NEAR/5 ("effectiv*")) OR (("follow*") NEAR/3 ("supervis*")) OR "transfer*"
 )
 NEAR
 ("employability")
) 
```
##### Phrase 4:

The basic structure is action + ICT + skill + employability. Some terms used in Phrase 1, like "abilit*" and "entrepreneurship$" are omitted here to reduce noise from research having to do with conditions within enterprises more generally, and not specifically with individuals' skills or employability

```Ceylon =
TS=
(
 ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "build*" OR "develop*" OR "relevan*")
  NEAR/5
  (
   ("information and communication technology" OR "ICT" OR "vocational" OR "technical" OR "technolog*" OR "comput*" OR "data*" OR "digital*" OR "information")
    NEAR/5
    ("skill*" OR "competen*" OR "literac*")
  )
   NEAR
   ("employab*" OR "employment" OR "job*")
)
```

## Target 4.5

> **4.5 By 2030, eliminate gender disparities in education and ensure equal access to all levels of education and vocational training for the vulnerable, including persons with disabilities, indigenous peoples and children in vulnerable situations**
>
> 4.5.1 Parity indices (female/male, rural/urban, bottom/top wealth quintile and others such as disability status, indigenous peoples and conflict-affected, as data become available) for all education indicators on this list that can be disaggregated

This target is interpreted to cover research about
* Reducing gender disparities in education
* Securing access to education and vocational training for vulnerable persons, including persons with disabilities and indigenous peoples

This query consists of 3 phrases.

##### Phrase 1:

The basic structure is action + gender equality + education

```Ceylon =
TS=
(
 (
  (
   ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "ensure*" OR "secure*") 
   NEAR/3 
    (
     ("gender" OR "girl*" OR "woman*" OR "women*" OR "female*" OR "boy$" OR "man" OR "men" OR "male")
     NEAR/5
      ("equit*" OR "equal*" OR "balanc*")
     )
    ) 	
    NEAR/3	
     (
      ("school*" OR "educat*" OR "vocational training" OR "student*")
     )
  )
)	
```
##### Phrase 2:

In this phrase, the basic structure is similar to phrase 1, but reversed to search for reduction of disparity: action + gender disparity + education

```Ceylon =
TS= 
(
 (
  (
   ("eliminat*" OR "reduc*" OR "remov*" OR "minimi*" OR "reduc*" OR "limit*" OR "lower*" OR "fight*" OR "combat*")
  ) 
  NEAR/5 
   (
    ("gender" OR "girl*" OR "woman*" OR "women*" OR "female*" OR "boy$" OR "man" OR "men" OR "male") 
    NEAR/5
    ("non-equit*" OR "non-equal*" OR "inequal*" OR "unequal*" OR "unbalanc*" OR "disparit*" OR "discriminat*" OR "obstacle*" OR "barrier*" OR "hindrance*" OR "hinder*")
   )
   NEAR/3
   ( 
    ("school*" OR "educat*" OR "vocational training" OR "student*")
   )
 )
)
```
##### Phrase 3:

We have not found an authoritative source defining "vulnerable groups", probably as who is considered to be vulnerable depends on the context and situation. Some of the terms were found in https://www.un.org/en/desa/leaving-no-one-behind, and others were found in articles from initial searches. "Elderly" can be vulnerable in some situations, but were omitted as they are not considered to be the primary target group for education. "Older" however, is included, to address the issues of lifelong learning. Terms like "migrant", "minority" and "rural" need not signify vulnerability, but were discovered to find research where these factors were seen as potential hindrances to accessing education, and were therefore included. The basic structure is action + access + education + vulnerable groups

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
    "access" OR "admission*" OR "admit*" OR "attend*" OR "inclusion*" OR "inclusiv*" OR "discriminat*" OR "non-discriminat*" OR "equitab*" OR "non-equit*" OR "barrier*" OR "obstacle*" OR "enter"
    )
   )
   NEAR/5
    (
     ("school*" OR "educat*" OR "vocational training")
    )
     NEAR
     (
      (
       ("person$" OR "people" OR "adult$" OR "child*" OR "student$" OR "youth$" OR "adolescent$")  
      NEAR/3
      ("disabled" OR "disabilit*" OR "unemployed" OR "older" OR "indigenous" OR "vulnerab*" OR "poor" OR "poverty" OR "displaced" OR "develop* contr*")
     )
     OR
     "disab*" OR "disadvantage*" OR "vulnerab*" OR "indigenous" OR "the poor" OR "refugee$" OR "asylum*" OR "displaced" OR "migrant*" OR "low* income*" OR "minorit*"  OR "marginal*" OR "slum*" OR "rural")
  )
 )
```

## Target 4.6

> **4.6 By 2030, ensure that all youth and a substantial proportion of adults, both men and women, achieve literacy and numeracy**
>
> 4.6.1 Proportion of population in a given age group achieving at least a fixed level of proficiency in functional (a) literacy and (b) numeracy skills, by sex

This target is interpreted to cover research about
		
* Achieving minimal or functional proficiency in literacy and numeracy skills
This is closely related to target 4.1, however, with the second phrase, more hits having to do with literacy and numeracy level, but not with school / educational system as such are found.

This query consists of 2 phrases.

##### Phrase 1:

The first phrase finds research about improving skills. The basic structure is action + level + skills

```Ceylon =
TS=
(
 ("increas*" OR "enhanc*" OR "ensure" OR "secure" OR "improv*" OR "achiev*" OR "reach*")
  NEAR/5
   (
    ("basi*" OR "fundamental*" OR "minim*" OR "core" OR "elementary" OR "functional" OR "adequate*") 
    NEAR
     ("proficien*" OR "skill*" OR "comprehen*" OR "abilit*")
      NEAR/5
       ("read*" OR "literacy" OR "literate" OR "math*" OR "numeracy" OR "numerate")
   )
)
```
##### Phrase 2:

In the second phrase we reverse the question and search for research about decreasing illiteracy, innumeracy and analphabetism. The basic structure is decrease + illiteracy etc. The seemingly similar search terms are truncated differently, as "innumera*" only returns noise with hits containing "innumerable".

```Ceylon =
TS=
(
 ("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "eliminat*")
  NEAR/3
   (" illitera*" OR "anal*abet*" OR "innumeracy*")
)
```

## Target 4.7

> **4.7 By 2030, ensure that all learners acquire the knowledge and skills needed to promote sustainable development, including, among others, through education for sustainable development and sustainable lifestyles, human rights, gender equality, promotion of a culture of peace and non-violence, global citizenship and appreciation of cultural diversity and of culture’s contribution to sustainable development**
>
> 4.7.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

This target is interpreted to cover research about
		
* Frameworks for education for sustainable development (ESD) and global citizenship (GCED) 
* Education in and about sustainable development, sustainable lifestyles, human rights, gender equality, peace, non-violence, global citizenship and cultural diversity
* Culture's contribution to sustainable development

This query consists of 3 phrases.

##### Phrase 1:

The search phrase GCED for Global Citizenship Education, retrieved from https://en.unesco.org/themes/education-sustainable-development/toolbox/implementation#esd-impl-46 was
tested, but only returned irrelevant hits from medical, mathematical and chemical research. After action terms, the phrase includes a wide range of terms concerning arenas and aspects of formalized education and learning, such as curriculum, teacher education etc. These are called frameworks in the interpretation above, but the term "framework" is not used in the search, as it leads to too much noise. As does "policy". The last part entails more and less detailed content of ESD and GCED. The basic structure is action + education + ESD/GCED

```Ceylon =
TS= 
(
 ("increas*" OR "ensur*" OR "enhanc*" OR "improv*" OR "develop*" OR "secur*" OR "attain*" OR "achiev*" OR "promot*" OR "implement*" OR "establish*" OR "empower*" OR "facilitat*")
 NEAR/5
 (
  ("educ*" OR "curricul*" OR "student assess*" OR "teaching" OR "teacher education" OR "teacher training" OR ("learn*" NEAR/5 "student*") OR "online learning" OR "professional learning")
 )
 NEAR/5
("sustainable development" OR "sustainable lifestyle$" OR "global citizen*" OR "glocal*" OR "human right*" OR "gender equality" OR "peace*" OR "non-violen*" OR "cultural divers*" OR "toleran*"
OR ("sustainability" NEAR/5 ("interdisciplinar*" OR "transdisciplinar*" OR "crossdisciplinar*" OR "cultural" OR "economic" OR "ecological" OR "participation" OR "agency" OR "responsibility" OR "ethic*" OR "wicked problem$" OR "complexity" OR "capacity for change" OR "transition$"))
 ) 
) 
```
##### Phrase 2:

The search phrase ESD for Education for Sustainable Development, retrieved from https://en.unesco.org/themes/education-sustainable-development was tested, but used alone returned too many irrelevant hits from other research fields. This phrase contains variants of education for sustainable development (ESD) and the structure is action + ESD.

```Ceylon =
TS= 
(
 ("increas*" OR "ensur*" OR "enhanc*" OR "improv*" OR "develop*" OR "secur*" OR "attain*" OR "achiev*" OR "promot*" OR "implement*" OR "establish*")
 NEAR/5
 (
  ("education for sustainab*" OR "education in sustainab*" OR "education on sustainab*" OR "sustainable development education" OR "sustainability education") 
 OR ("whole school" OR "teaching") NEAR ("sustainab*" OR "ESD" NEAR/5 "educat*")
 )
) 
```
##### Phrase 3:

This phrase is related to searches in SDG 11 about cultural heritage, and likely to have some overlap, yet it is included here as culture's contribution to sustainable development is directly addressed in the target. The basic structure is culture + contribution + sustainable development.

```Ceylon =
TS= 
(
 (
  ("culture*" OR "cultural")
  NEAR/5
  ("contribut*" OR "influen*" OR "impact*" )
 )
  NEAR 
  "sustainable development"
 )
```
## Target 4.a

> **4.a Build and upgrade education facilities that are child, disability and gender sensitive and provide safe, non-violent, inclusive and effective learning environments for all**
>
> 4.a.1 Proportion of schools offering basic services, by type of service

This target is interpreted to cover research about
* Safe and inclusive education facilities
* Effective learning environments in schools
* Access to basic services such as electricity, internet, drinking water and sanitation facilities in schools

We understand the target to be concerned chiefly with facilities for primary and secondary education. We do not include higher education, education and learning taking place in other contexts such as hospitals, prisons, or workplaces, or virtual/online learning arenas.

This query consists of 3 phrases.

##### Phrase 1:

This phrase finds research on ensuring safe and inclusive schools and education facilities. The basic structure is action + school + safe and inclusive.

```Ceylon =
TS=
(
 ("build*" OR "design*" OR "upgrad*" OR "establish*" OR "improv*" OR "ensur*" OR "provide*")
 NEAR/5
 (
  ("school*" OR "education facilit*")
  NEAR/5
  ("safe*" OR "secure*" OR "non-violen*" OR "inclus*" OR (("sensitive")NEAR/5 "child*" OR "disability" OR "gender"))
 )
)
```
##### Phrase 2:

This phrase focuses on effective learning environments in schools. The basic structure is provide + effective learning environment + school. 

```Ceylon =
TS=
(
 ("build*" OR "design*" OR "upgrad*" OR "establish*" OR "improv*" OR "ensur*" OR "provid*") 
 NEAR/5
 (
  ("learning environment*")
   NEAR/5
   ("effective")
  )
  AND
  ("primary school*" OR "elementary school*" OR "primary educat*" OR "middle school*" OR "secondary school*" OR "secondary education*" OR 
      "school" OR "education" OR "learner*")
)
```
##### Phrase 3:

This phrase focuses on access to basic services in schools. The terms for basic services in schools are taken and adapted from: http://tcg.uis.unesco.org/wp-content/uploads/sites/4/2019/08/sdg4-global-indicators-4.a.pdf The basic structure is school + access + basic services.

```Ceylon =
TS=
(
 (
  ("school*"OR "education* facility" OR "education* facilities")
  NEAR
   (
    ("access*")
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

This query consists of 1 phrase.

##### Phrase 1:

There are no actions terms included, as there are so few hits they are considered to be of potential interest even without action terms. Scholarships must be used in plural form, as it would otherwise also include "work done by scholars", which would confuse the logic of the search entirely. The basic structure is scholarships + student/education + developing countries.

```Ceylon =
TS=
(
 ("scholarships*" OR "scholarship program*" OR "fellowship*" OR "sponsorship*" OR "exchange program*" OR "grant*") 
  NEAR
  ("student*" OR "higher education" OR "trainee*" OR "student exchange*" OR "student mobility*" OR (("information and communication$ technology" OR "technic*" OR "engineer*" OR "science" OR "scientific") NEAR ("program*")))
 AND
  ("least developed countr*" OR "least developed nation$"OR "developing countr*" OR "developing nation$" OR "developing states" OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "small island developing states" OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "St Lucia" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa" OR "Sao Tome" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "Tuvalu" OR "Vanuatu" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands" OR (("Africa*" OR "Algeria" OR "Angola" OR "Benin" OR "Botswana" OR "Burkina Faso" OR "Burundi" OR "Cameroon" OR "Canary Islands" OR "Cape Verde" OR "Central African Republic" OR "Chad" OR "Comoros" OR "Congo" OR "Democratic Republic of Congo" OR "Djibouti" OR "Egypt" OR "Equatorial Guinea" OR "Eritrea" OR "Ethiopia" OR "Gabon" OR "Gambia" OR "Ghana" OR "Guinea" OR "Guinea Bissau" OR "Ivory Coast" OR "Cote d’Ivoire" OR "Jamahiriya" OR "Kenya" OR "Lesotho" OR "Liberia" OR "Libya" OR "Libia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mauritius" OR "Mayote" OR "Morocco" OR "Mozambique" OR "Mocambique" OR "Namibia" OR "Niger" OR "Nigeria" OR "Principe" OR "Reunion" OR "Rwanda" OR "Sao Tome" OR "Senegal" OR "Seychelles" OR "Sierra Leone" OR "Somalia" OR "South Africa" OR "St Helena" OR "Sudan" OR "Swaziland" OR "Tanzania" OR "Togo" OR "Tunisia" OR "Uganda" OR "Western Sahara" OR "Zaire" OR "Zambia" OR "Zimbabwe") NOT ("guinea pig" OR "guinea pigs" OR "aspergillus niger")
 ))
)
```

## Target 4.c

> **4.c By 2030, substantially increase the supply of qualified teachers, including through international cooperation for teacher training in developing countries, especially least developed countries and small island developing States**
>
> 4.c.1 Proportion of teachers with the minimum required qualifications, by education level

This target is interpreted to include research about
* Increasing the number of qualified teachers
* Teacher training in developing countries
* International cooperation for teacher training

This query consists of 4 phrases.

##### Phrase 1:

This phrase finds research about increasing the number of qualified teachers. However, neither "qualified teacher*" nor "professional development" are included in the search as they predominantly return hits about how teachers who are already qualified can improve, whereas the target is interpreted to concern increasing the number who attain the minimum required qualification. The basic structure is action + qualified/certified teachers.

```Ceylon =
TS= 
 (
  ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up" OR "reduc*" OR "decreas*")
   NEAR
   (
    ("teach* qualification$" OR "teach* certific*" OR "certif* teacher*" OR "unqualified teacher*")
   )
 )
```
##### Phrase 2:

This phrase finds articles about teacher education in developing countries, especially least developed countries and small island developing states. The basic structure is teacher + education + least developed countries or small island developing states. 

```Ceylon =
TS=
(
 (
  ("teacher")
  NEAR
   ("educat*" OR "train*")
  ) 
  NEAR
  ("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR "developing states" OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "small island developing states" OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "St Lucia" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa" OR "Sao Tome" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "Tuvalu" OR "Vanuatu" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands")
)
```
##### Phrase 3:

This phrase finds articles about the level of qualification for teachers. The basic structure is teacher + level of qualification.

```Ceylon =
TS=
(
 ("teacher*")
  NEAR
  ("level of qualification*" OR "qualification level")
)
```
##### Phrase 4:

This phrase finds articles about international cooperation for teacher education. Much research is concerned with globalization and internationalization as aspects of teacher education, therefore "program*" and related terms is included to find specific projects or efforts. The basic structure is teacher + education + international cooperation.

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
 OR "international teacher education program*"
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
EHS. Internal review first draft: KH, HMB, CSA (January 2022). Workshop external input (February 2022). Internal review second draft: CSA, ML (March 2022).

## 5. Footnotes
<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)
