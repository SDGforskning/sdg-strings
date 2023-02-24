# Search query for SDG 4 - Quality Education, Bergen action-approach.

Ensure inclusive and equitable quality education and promote lifelong learning opportunities for all.

**Current status**: This string is currently a finished version.

**Contents**

1. Full query in copy-pasteable format
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes

## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here: https://www.webofscience.com/wos/woscc/summary/433e2561-fc3b-472e-b8c2-b1466fb72766-57b893e7/relevance/1 (no filters; all years)

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 4 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 4 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f10)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters). For African countries (target 4.b), we adapted a filter developed by <a id="Africancountries">[Pienaar et al. (2011)](#f9)</a>.

## 3. Targets

### Target 4.1

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

#### Phrase 1

The basic structure is *action + completion + school education*.

In many medical and other studies that are not concerned with education as such, having completed a specific level of education is used as a parameter. To reduce the number of such studies, we have used many variants of the verb complete, but avoided "completed" and "complete*".

```py
TS=
(
  (
    ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better*" OR "ensure" OR "attain" OR "achiev*")
    NEAR/5
      ("complete" OR "completing" OR "completes" OR "completion" OR "school completion" OR "finish*" OR "graduate" OR "graduation")
  )
  NEAR/5
      ("primary school*" OR "elementary school*" OR "primary educat*"
      OR "middle school*" OR "secondary school*" OR "secondary education*"
      OR (("school" OR "education") NEAR/3 ("boys" OR "girls" OR "kids" OR "child*"))
      )
)
```

#### Phrase 2

The basic structure is *action + dropout + school education*.

In this phrase we reverse the concept of increasing school completion, and focus on reducing dropouts.

```py
TS=
(
  (
    ("prevent*" OR "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "lower$" OR "improv*")
    NEAR/5
      ("dropout*" OR "drop-out*" OR "drop out" OR "dropping out" OR "quit" OR "early school-leaving")
  )
  NEAR/5
      ("primary school*" OR "elementary school*" OR "primary educat*"
      OR "middle school*" OR "secondary school*" OR "secondary education*"
      OR (("school" OR "education") NEAR/3 ("boys" OR "girls" OR "kids" OR "child*"))
      )
)
```
#### Phrase 3

The basic structure is *action + access + school + free/equitable/quality*.

"Quality education" is a broad term, and the short name of SDG 4.  As specified by UNESCO in its SDG Resources for Educators (<a id="unescoquality">[UNESCO, n.d.a](#f2)</a>):
> "Quality education specifically entails issues such as appropriate skills development, gender parity, provision of relevant school infrastructure, equipment, educational materials and resources, scholarships or teaching force."

These are all addressed in the subsequent targets, therefore "quality education" is not elaborated on further here.

```py
TS=
(
    (
      ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher"
      OR "scal* up" OR "build*" OR "expand"  OR "accelerat*"
      OR "ensure" OR  "attain*" OR "achiev*"
      )  
      NEAR/5 ("access*" OR "enter*" OR "entry" OR "enroll*" OR "admission" OR "admit*")
    )
    NEAR/15
      (
        ("primary school*" OR "elementary school*" OR "primary educat*"
        OR "middle school*" OR "secondary school*" OR "secondary education"
        )
        NEAR/5 ("free" OR "equit*" OR "quality")
      )
)  
```
#### Phrase 4

The basic structure is *action + level + skill + reading and mathematics*.

We considered including terms for primary and secondary education, but too many relevant hits were excluded, and we deem the delimitation unnecessary.

```py
TS=
(
  (
    (
      ("increas*" OR "enhanc*" OR "ensure" OR "secure" OR "improv*" OR "achiev*")
      NEAR/5
        (
          ("basic" OR "fundamental*" OR "minim*" OR "basic*" OR "core" OR "elementary")
          NEAR/10 ("proficienc*" OR "skill*" OR "comprehen*" OR "literac*" OR "read*" OR "mathematic*" OR "math" OR "maths" OR "numera*")
        )
    )
    NEAR/15 ("read" OR "reading" OR "mathematic*" OR "math" OR "maths" OR "numera*")
  )
  AND ("school" OR "student$" OR "boys" OR "girls" OR "kids" OR "child*")
)
```

### Target 4.2

> **4.2 By 2030, ensure that all girls and boys have access to quality early childhood development, care and pre‑primary education so that they are ready for primary education**
>
> 4.2.1 Proportion of children aged 24–59 months who are developmentally on track in health, learning and psychosocial well-being, by sex
>
> 4.2.2 Participation rate in organized learning (one year before the official primary entry age), by sex

This target is interpreted to cover research about

* Ensuring access to institutionalized, early childhood education (and care)
* Readiness for primary education

This query consists of 2 phrases.

#### Phrase 1

The basic structure is *action + access + early care*.

The search term "care" is not used alone as it would give too many hits that are only indirectly relevant to readiness for and participation in organized learning. Variants of daycare were considered, but returned too many hits not considered relevant to the target. The basic structure is improve access / remove obstacles + early childhood education and care. Some agricultural terms which occur in combinations with "nurser*" had to be excluded with NOT.

```py
TS=
(
  (
    ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher"
    OR "overcome" OR  "ensure" OR "attain*" OR "achiev*"
    OR "decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limiting" OR "limited" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*"
    )
    NEAR/5
      ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*")
  )
  NEAR/5
      ("early childhood care" OR "kindergarten" OR "pre-kindergarten*" OR "nurser*" OR "pre-primary*" OR "pre school*" OR "preschool*"
      OR (("early childhood" OR "under five$") NEAR/3 "education")
      )
)
NOT
TS= ("pig*" OR "plant*" OR "fish*")

```
#### Phrase 2

The basic structure is *school readiness // child development + school entry*.

```py
TS=
(
  "school readiness"
  OR
    (
      ("ready" OR "readiness" OR "prepared*")
      NEAR/5
        ("primary education*" OR "primary school*" OR "elementary school*" OR "first grade" OR "1st grade*")
    )
  OR
    (
      ("development*" NEAR/5 ("children*" OR "under-five*" OR "early childhood"))
      NEAR/5 "school entry"
   )
)
```

### Target 4.3

> **4.3 By 2030, ensure equal access for all women and men to affordable and quality technical, vocational and tertiary education, including university**
>
> 4.3.1 Participation rate of youth and adults in formal and non-formal education and training in the previous 12 months, by sex

This target is interpreted to cover research about:
* Equal access for all to technical, vocational and tertiary education, including universities

We have interpreted the target widely, and included search terms to identify research on discrimination, barriers etc. that may prevent or hinder access. We have also included post-secondary education, a level between upper secondary and tertiary education which does not necessarily give access to tertiary education, and is often practically or vocationally, as opposed to theoretically or generally, oriented (according to UNESCO's International Standard Classification of Education (ISCED); <a id="isced">[UNESCO, 2012](#f3)</a>).

This query consists of 3 phrases. The first two phrases contain many of the same terms, but they are combined differently to reduce noise. In particular, combinations of `access` with `university or education` can result in a large quantity of articles about open access publishing and universities, which are not relevant here. To avoid this, in phrase 1 "access" is limited by the inclusion of action terms, and the condition that `university` must be near `admission$ OR enrol*`. In phrase 2, "access" is limited by its combination with terms to do with equality/discrimination, allowing us to also find publications that do not mention enrolment or admission specifically.

#### Phrase 1

The basic structure is *action + access + higher education*

```py
TS=
(
  (
    (
      ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "ensur*" OR "secure" OR "initiative$" OR "intervention$")
      NEAR/5
        ("access*" OR "inclusion*" OR "inclusiv*" OR "non-discriminat*" OR "equitab*" OR "equal*" OR "afford*")
    )
  OR
    (
      ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting" OR "alleviat*"
      OR "address*" OR "tackl*" OR "combat*" OR "fight*" OR "prevent*" OR "avoid*"
      OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
      OR "improv*" OR "manag*"
      )
      NEAR/5
        ("barrier$" OR "obstacle$" OR "non-equitiab*" OR "inequal*" OR "discriminat*")
    )
  )
  NEAR/15
      ("higher education"
      OR (("university" OR "universities" OR "college$") NEAR/5 ("admission$" OR "enrol*"))
      OR
        (
          ("technic*" OR "vocation*" OR "tertiar*" OR "university" OR "postsecondary" OR "post secondary")
          NEAR/3 ("education" OR "training" OR "school*" OR "learning")
        )
      )
)

```
#### Phrase 2

The basic structure is *action + equality + higher education*

```py
TS=
(
  (
    (
        (
          ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "ensur*" OR "secure" OR "initiative$" OR "intervention$")
          NEAR/5
              ("inclusion*" OR "inclusiv*" OR "non-discriminat*" OR "equitab*" OR "equal*")
        )
      OR
        (
          ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting" OR "alleviat*"
          OR "address*" OR "tackl*" OR "combat*" OR "fight*" OR "prevent*" OR "avoid*"
          OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
          OR "improv*" OR "manag*"
          )
          NEAR/5
              ("barrier$" OR "obstacle$" OR "non-equitiab*" OR "inequal*" OR "discriminat*")
        )
    )
    NEAR/15 ("access")
  )
  NEAR/15
      ("university" OR "universities" OR "higher education" OR "college$"
      OR
        (
          ("technic*" OR "vocation*" OR "tertiar*" OR "postsecondary" OR "post secondary")
          NEAR/3 ("education" OR "training" OR "school*" OR "learning")
        )
      )
)
```

#### Phrase 3

```py
TS= "inclusive higher education"
```

### Target 4.4

> **4.4 By 2030, substantially increase the number of youth and adults who have relevant skills, including technical and vocational skills, for employment, decent jobs and entrepreneurship**
>
> 4.4.1 Proportion of youth and adults with information and communications technology (ICT) skills, by type of skill

This target is interpreted to cover research about

* Increasing the number of youths and adults who have relevant skills for employment and entrepreneurship
* Improvement of ICT skills and employability

This query consists of 4 phrases. The first two cover skills at an overriding level, the third core skills as defined by the UN International Labor Organisation, and the fourth ICT skills. In order to limit the search to research concerning opportunities for employment, and avoid articles about employees/employers and their (needs for) development in jobs and workplaces, only "employability" and "employment" are used alongside jobs and entrepreneurship. The term "work" is not included as it gives too much noise.

#### Phrase 1

The basic structure is *action + skills + employability/entrepreneurship*

```py
TS=
(
  (
    ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "build*" OR "develop*")
    NEAR/5
      ("skill$" OR "abilit*" OR "competenc*" OR "literac*")
  )
  NEAR/5 ("employability*" OR "employment" OR "decent job$" OR "decent work" OR "entrepreneurship$")
)
```
#### Phrase 2

This phrase finds research talking about skills, competencies etc. in relation to reducing unemployment. The basic structure is *action + unemployment + skills*

```py
TS=
(
  (
    ("reduc*" OR "decreas*" OR "lower*"  OR "prevent*" OR "minimi*" OR "limit*" OR "eliminat*")
    NEAR/5
        ("unemploy*" OR "underemploy*")
  )
  NEAR/5 ("skill$" OR "abilit*" OR "competenc*" OR "literac*" OR "literate")
 )
 ```

#### Phrase 3

The basic structure is *core and transferable skills + employability*

Types of skills included here are taken from an ILO publication on youth skills for employability (<a id="iloskills">[Brewer 2013](#f4)</a>). Employment is omitted as a search term here, as it leads to irrelevant results concerned with the use (="employment") of the skills.

```py
TS=
(
  (
    "read*" OR "writ*" OR "comput*" OR "literacy" OR "numeracy"
    OR (("basic technolog*" OR "speciali$ed") NEAR/3 ("skills" OR "knowledge"))
    OR "learn and adapt"
    OR (("listen*" OR "communicat*") NEAR/3 ("skills" OR "effective*"))
    OR "think creatively" OR "creative thinking" OR "solve problem$" OR "problem-solv*"
    OR ("interact*" NEAR/3 ("co-work*" OR "colleague$"))
    OR (("work" OR "working") NEAR/3 ("team*" OR "group*"))
    OR ("leader*" NEAR/5 ("skills" OR "effectiv*"))
    OR ("follow*" NEAR/3 "supervis*")
    OR ("transfer*" NEAR/3 "skills")
  )
  NEAR/15 "employability"
)
```
#### Phrase 4

The basic structure is *action + ICT + skill + employability*.

Some terms used in Phrase 1, like `"abilit*"` and `"entrepreneurship$"` are omitted here to reduce noise from research having to do with conditions within enterprises more generally, and not specifically with individuals' skills or employability

```py
TS=
(
  (
    ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher" OR "build*" OR "develop*")
    NEAR/5
      (
        ("information and communication technology" OR "ICT" OR "vocational" OR "technical" OR "technolog*" OR "comput*" OR "data*" OR "digital*" OR "information")
        NEAR/5
            ("skill*" OR "competen*" OR "literac*")
      )
  )
  NEAR/15 ("employab*" OR "employment" OR "job$" OR "decent work")
)
```

### Target 4.5

> **4.5 By 2030, eliminate gender disparities in education and ensure equal access to all levels of education and vocational training for the vulnerable, including persons with disabilities, indigenous peoples and children in vulnerable situations**
>
> 4.5.1 Parity indices (female/male, rural/urban, bottom/top wealth quintile and others such as disability status, indigenous peoples and conflict-affected, as data become available) for all education indicators on this list that can be disaggregated

This target is interpreted to cover research about
* Reducing gender disparities in education
* Securing access to education and vocational training for vulnerable persons, including persons with disabilities and indigenous peoples

This query consists of 3 phrases.

#### Phrase 1

The basic structure is *action + gender equality + education*

```py
TS=
(
  (
    ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "ensur*" OR "secure" OR "support*")
    NEAR/5
        (
          ("gender" OR "girl*" OR "woman*" OR "women*" OR "female*" OR "boy$" OR "man" OR "men" OR "male")
          NEAR/5
              ("equit*" OR "equal*" OR "balanc*")
        )
    ) 	
    NEAR/5 ("school*" OR "educat*" OR "vocational training" OR "student*")
)
```

#### Phrase 2

In this phrase, the basic structure is similar to phrase 1, but reversed to search for reduction of disparity: *action + gender disparity + education*

```py
TS=
(
  (
    ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting" OR "alleviat*"
    OR "address*" OR "tackl*" OR "combat*" OR "fight*" OR "prevent*" OR "avoid*"
    OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
    OR "improv*"
    )
    NEAR/5
      (
        ("gender" OR "girl*" OR "woman*" OR "women*" OR "female*" OR "boy$" OR "man" OR "men" OR "male")
        NEAR/5
            ("non-equit*" OR "non-equal*" OR "inequal*" OR "unequal*" OR "unbalanc*" OR "imbalanc*" OR "disparit*" OR "discriminat*"
            OR "obstacle*" OR "barrier*" OR "hindrance*" OR "hinder*"
            )
      )
  )
  NEAR/5
      ("school*" OR "educat*" OR "vocational training" OR "student*")
)
```

#### Phrase 3

The basic structure is *action + access + education + vulnerable groups*

"Vulnerable groups" are mentioned in several SDGs, but can be difficult to define for a search string - who is considered vulnerable may depend on the context and situation. To get a general outline of who is considered "vulnerable" we have consulted several UN sources on the topic (<a id="Blanchard">[Blanchard et al., 2017](#f5)</a>; <a id="UNOHC">[Office of the High Commissioner, n.d.](#f6)</a>; <a id="UNracism">[United Nations, n.d.](#f7)</a>). Most terms were taken from these, and adapted so that the terms work combined with terms relevant for SDG4. `rural` was not a term included in the UN documents and need not signify vulnerability, but we found works suggesting that it is a potential hindrance to accessing education, and was therefore included.

```py
TS=
(
  (
    (
      (
        ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "ensure*" OR "secure" OR "support*")
        NEAR/5
            ("access" OR "admission*" OR "admit*" OR "attend*" OR "entry" OR "enrol*"
            OR "inclusion*" OR "inclusiv*" OR "non-discriminat*" OR "equitab*"
            )
      )
    OR
      (
        ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limited" OR "limiting" OR "alleviat*"
        OR "address*" OR "tackl*" OR "combat*" OR "fight*" OR "prevent*" OR "avoid*"
        OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*"
        OR "improv*"
        )
        NEAR/5
            ("discriminat*" OR "non-discriminat*" OR "non-equit*" OR "disparit*"
            OR "barrier*" OR "obstacle*"
            )
      )
    )
    NEAR/5 ("school*" OR "educat*" OR "vocational training")
  )
  NEAR/15
      (
        (
          ("person$" OR "people" OR "adult$" OR "child*" OR "student$" OR "youth$" OR "adolescent$")  
          NEAR/3
              ("disabled" OR "disabilit*" OR "unemployed" OR "older" OR "elderly"
              OR "poor" OR "poorest" OR "poverty" OR "disadvantaged" OR "vulnerab*" OR "displaced" OR "marginali$ed" OR "developing countr*"
              )
        )
     OR "disab*" OR "disadvantage*" OR "vulnerab*" OR "indigenous" OR "the poor"
     OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
     OR "refugee$" OR "asylum*" OR "displaced" OR "migrant*" OR "low* income*"
     OR "minorit*"  OR "marginal*" OR "slum*" OR "rural"
     )
)
```

### Target 4.6

> **4.6 By 2030, ensure that all youth and a substantial proportion of adults, both men and women, achieve literacy and numeracy**
>
> 4.6.1 Proportion of population in a given age group achieving at least a fixed level of proficiency in functional (a) literacy and (b) numeracy skills, by sex

This target is interpreted to cover research about achieving minimal or functional proficiency in literacy and numeracy skills.

This is closely related to target 4.1, however, with the second phrase, we find more results about literacy and numeracy level, but not with school / educational system.

This query consists of 2 phrases.

#### Phrase 1

The first phrase finds research about improving skills. The basic structure is *action + level + skills*.

```py
TS=
(
    (
      ("increas*" OR "enhanc*" OR "ensure" OR "secure" OR "improv*" OR "achiev*" OR "reach*")
      NEAR/5
        (
          ("basic" OR "fundamental*" OR "minim*" OR "core" OR "elementary" OR "functional" OR "adequate*")
          NEAR/10 ("proficienc*" OR "skill*" OR "comprehen*" OR "abilit*" OR "literac*")
        )
    )
    NEAR/5 ("read" OR "reading" OR "literate" OR "mathematic*" OR "math" OR "maths" OR "numeracy" OR "numerate")
)
```

#### Phrase 2

In the second phrase we reverse the question and search for research about decreasing illiteracy, innumeracy and analphabetism. The basic structure is *decrease + illiteracy*. 

```py
TS=
(
  ("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting"
  OR "mitigat*" OR "tackl*" OR "alleviat*" OR "lowering" OR "lowers" OR "lowered" OR "fight*" OR "combat*" OR "eliminat*"
  OR "improv*"
  )
  NEAR/3
      ("illitera*" OR "analfabet*" OR "analphabet*" OR "innumeracy" OR "innumerate*")
)
```

### Target 4.7

> **4.7 By 2030, ensure that all learners acquire the knowledge and skills needed to promote sustainable development, including, among others, through education for sustainable development and sustainable lifestyles, human rights, gender equality, promotion of a culture of peace and non-violence, global citizenship and appreciation of cultural diversity and of culture’s contribution to sustainable development**
>
> 4.7.1 Extent to which (i) global citizenship education and (ii) education for sustainable development are mainstreamed in (a) national education policies; (b) curricula; (c) teacher education; and (d) student assessment

This target is interpreted to cover research about

* Frameworks for education for sustainable development (ESD) and global citizenship (GCED)
* Education in and about sustainable development, sustainable lifestyles, human rights, gender equality, peace, non-violence, global citizenship and cultural diversity
* Culture's contribution to sustainable development

This query consists of 3 phrases.

#### Phrase 1

The basic structure is *action + education + sustainability/GCED*.

 <a id="unescogced">[UNESCO (n.d.b)](#f8)</a> was used as a source of terms. The search term `GCED` for Global Citizenship Education was tested, but only returned irrelevant hits from medical, mathematical and chemical research. After action terms, the phrase includes a wide range of terms concerning arenas and aspects of formalized education and learning, such as curriculum, teacher education etc. These are called frameworks in the interpretation above, but the term "framework" is not used in the search, as it leads to too much noise. As does "policy". The last part entails more and less detailed content of ESD and GCED.

```py
TS=
(
  (
    ("increas*" OR "ensur*" OR "enhanc*" OR "improv*" OR "develop*" OR "secur*"
    OR "attain*" OR "achiev*" OR "promot*" OR "implement*" OR "establish*" OR "empower*" OR "facilitat*"
    )
    NEAR/5
        ("educat*" OR "curricul*"
        OR "student assess*" OR "teaching" OR "teacher education" OR "teacher training"
        OR "online learning" OR "professional learning"
        OR ("learn*" NEAR/5 "student*")
        )
  )
  NEAR/5
      ("sustainable development" OR "sustainable lifestyle$"
      OR "global citizen*" OR "glocal*"
      OR "human right*" OR "gender equality" OR "peace*" OR "non-violen*"
      OR "cultural divers*" OR "toleran*"
      OR
          ("sustainability"
          NEAR/5
              ("interdisciplinar*" OR "transdisciplinar*" OR "crossdisciplinar*" OR "cultural" OR "economic" OR "ecological"
              OR "participation" OR "agency" OR "responsibility"
              OR "ethic*" OR "wicked problem$" OR "complexity"
              OR "capacity for change" OR "transition$"
              )
          )
      )
)
```

#### Phrase 2

The basic structure is *action + ESD*.

The search phrase `ESD` for Education for Sustainable Development was tested, but used alone returned too many irrelevant hits from other research fields. This phrase contains variants of education for sustainable development (ESD).

```py
TS=
(
  ("increas*" OR "ensur*" OR "enhanc*" OR "improv*" OR "develop*" OR "secur*" OR "attain*" OR "achiev*" OR "promot*" OR "implement*" OR "establish*")
  NEAR/5
      ("education for sustainab*" OR "education in sustainab*" OR "education on sustainab*" OR "sustainable development education" OR "sustainability education"
      OR (("whole school" OR "teaching") NEAR/5 (("sustainab*" OR "ESD") NEAR/5 "educat*"))
      )
)
```

#### Phrase 3

This phrase is related to searches in SDG 11 about cultural heritage, and likely to have some overlap, yet it is included here as culture's contribution to sustainable development is directly addressed in the target. The basic structure is *culture + contribution + sustainable development*.

```py
TS=
(
  (
    ("culture*" OR "cultural")
    NEAR/5 ("contribut*" OR "influen*" OR "impact*")
  )
  NEAR/5 "sustainable development"
)
```


### Target 4.a

> **4.a Build and upgrade education facilities that are child, disability and gender sensitive and provide safe, non-violent, inclusive and effective learning environments for all**
>
> 4.a.1 Proportion of schools offering basic services, by type of service

This target is interpreted to cover research about
* Safe and inclusive education facilities
* Effective learning environments in schools
* Access to basic services such as electricity, internet, drinking water and sanitation facilities in schools

We understand the target to be concerned chiefly with facilities for primary and secondary education. We do not include higher education, education and learning taking place in other contexts such as hospitals, prisons, or workplaces, or virtual/online learning arenas.

This query consists of 3 phrases.

#### Phrase 1

This phrase finds research on ensuring safe and inclusive schools and education facilities. The basic structure is *action + school + safe and inclusive*.

```py
TS=
(
  ("build*" OR "design*" OR "upgrad*" OR "establish*" OR "improv*" OR "ensur*" OR "provid*")
  NEAR/5
      (
        ("school*" OR "education facilit*")
        NEAR/5
            ("safe*" OR "secure*" OR "non-violen*" OR "inclus*"
            OR ("sensitive" NEAR/5 ("child*" OR "disability" OR "gender"))
            )
      )
)
```

#### Phrase 2

This phrase focuses on effective learning environments in schools. The basic structure is *provide + effective learning environment + school*.

```py
TS=
(
  (
    ("build*" OR "design*" OR "upgrad*" OR "establish*" OR "improv*" OR "ensur*" OR "provid*")
    NEAR/5
        ("learning environment*" NEAR/5 "effective")
  )
  AND
    ("primary school*" OR "elementary school*" OR "primary educat*"
    OR "middle school*" OR "secondary school*" OR "secondary educat*"
    OR "school" OR "education" OR "learner*"
    )
)
```

#### Phrase 3

This phrase focuses on improving access to basic services in schools. The basic structure is *action + access + basic services + schools*.

The terms for basic services in schools are taken and adapted from <a id="unescotcg">[UNESCO Institute for statistics (2018)](#f11)</a>

```py
TS=
(
 (
  ("improv*" OR "secur*" OR "ensur*" OR "provide" OR "build*")
  NEAR/3
    ("access*"
    NEAR/5
      ("electricity" OR "electrical supply" OR "modern energy" OR "internet" OR "computer*" OR "ICT facilit*" OR "adapted infrastructure*" OR 
      "adapted material*" OR "universal design" OR ("infrastructure" NEAR/5 "disab*")
      OR "drinking water" OR "sanitation" OR "handwash*" OR "hand wash*" OR "WASH facilities" OR "toilet$")
     )
  )
  NEAR/15
  ("school*" OR "education* facility" OR "education* facilities")
 ) 
```

### Target 4.b

> **4.b By 2020, substantially expand globally the number of scholarships available to developing countries, in particular least developed countries, small island developing States and African countries, for enrolment in higher education, including vocational training and information and communications technology, technical, engineering and scientific programmes, in developed countries and other developing countries**
>
> 4.b.1 Volume of official development assistance flows for scholarships by sector and type of study

This target is interpreted to cover research about the availability of scholarships to students from developing countries and African countries.

This query consists of 1 phrase.

#### Phrase 1

The basic structure is *scholarships + student/education + developing countries/African countries*.

There are no actions terms included, as there are so few results they are considered to be of potential interest even without action terms. Scholarships must be used in plural form, as it would otherwise also include "work done by scholars", which would confuse the logic of the search.

```py
TS=
(
  (
    ("scholarships" OR "scholarship program*" OR "fellowship*" OR "sponsorship*" OR "exchange program*" OR "grant$")
    NEAR/15
        ("student*" OR "higher education" OR "trainee*" OR "student exchange$" OR "student mobility")
  )
AND
  ("least developed countr*" OR "least developed nation$"
  OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
  OR "less developed countr*" OR "less developed nation$"
  OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
  OR "underserved countr*" OR "underserved nation$"
  OR "deprived countr*" OR "deprived nation$"
  OR "middle income countr*" OR "middle income nation$"
  OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
  OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
  OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
  OR  "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
  OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
  OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
  OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palastinian$" OR "yugoslavia*" OR "turkish"
  OR "Africa*" OR "Algeria*" OR "Angola*" OR "Benin" OR "beninese" OR "Botswana*" OR "Burkina Faso" OR "Burkina Fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Cameroon*" OR "Canary Islands" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "Central African Republic" OR "Chad" OR "Congo" OR "congolese" OR "Djibouti*" OR "Egypt*" OR "Equatorial Guinea" OR "Eritrea*" OR "Ethiopia*" OR "Gabon*" OR "Gambia*" OR "Ghana*" OR "Guinea" OR "guinean$" OR "Guinea Bissau" OR "Ivory Coast" OR "Cote d’Ivoire" OR "Jamahiriya" OR "Kenya*" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Libya*" OR "Libia" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania" OR "mauritanian$" OR "Mauritius" OR "mauritian$" OR "Mayotte" OR "Morocco" OR "moroccan$" OR "Mozambique" OR "Mocambique" OR "mozambican$" OR "Namibia*" OR "Niger" OR "Nigeria*" OR "Principe" OR "Reunion" OR "Rwanda*" OR "Sao Tome" OR "Senegal*" OR "Seychelles" OR "seychellois*" OR "Sierra Leone*" OR "Somalia*" OR "South Africa*" OR "St Helena" OR "Sudan*" OR "Swaziland*" OR "Tanzania*" OR "Togo" OR "togolese" OR "tongan" OR "Tunisia*" OR "Uganda*" OR "Western Sahara" OR "Zaire" OR "Zambia*" OR "Zimbabwe*"
  )
)
```

### Target 4.c

> **4.c By 2030, substantially increase the supply of qualified teachers, including through international cooperation for teacher training in developing countries, especially least developed countries and small island developing States**
>
> 4.c.1 Proportion of teachers with the minimum required qualifications, by education level

This target is interpreted to include research about
* Increasing the number of qualified teachers and reducing teacher attrition / shortage
* Increasing/improving teacher training in developing countries, including via international cooperation for teacher training

This query consists of 3 phrases.

#### Phrase 1

The basic structure is *action + teachers/qualified teachers*.

This phrase finds research about increasing the number of qualified teachers.

```py
TS=
(
  (
    ("increas*" OR "expand*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up" OR "ensur*" OR "address*")
        NEAR/5
        ("supply" OR "coverage" OR "enough" OR "quantity" OR "recruit*" OR "retention" OR "lack of" OR "turnover" OR "shortage" OR "share of")
   ) 
   NEAR/5 ("teacher$" OR ("qualif*" NEAR/3 "teach*"))
)
```

#### Phrase 2

The basic structure is *action + unqualified teachers/teacher shortage*.

This phrase finds research about reducing teacher turnover, attrition and shortage

```py
TS=
(
  ("reduc*" OR "decreas*" OR "avoid*" OR "prevent*")
  NEAR/5
      ("teacher$" NEAR/3 ("unqualified" OR "turnover" OR "attrition" OR "shortage$"))
)
```

#### Phrase 3

This phrase finds research about improving teacher education in developing countries, including through international cooperation. As there are few hits, and they are hard to capture, we use a wide version of action terms in this string, not strictly limited to verbs.
The basic structure is *action OR cooperation + teacher education + countries*.

```py
TS=
(
 (
  ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "upgrad*" OR "scal* up"
   OR "study abroad*" OR "exchange" OR "mobility" OR
   (
    ("international" OR "development" OR "global" OR "cross")
       NEAR/3
       ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$" OR "program$")
    )
   OR "international teacher education program*" OR "international teacher training program*"
  )
   NEAR/15 ("teacher training" OR "teacher education" OR "teacher qualification*" OR "qualifi* teacher$")
 ) 
 AND
    ("least developed countr*" OR "least developed nation$"
    OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
    OR "less developed countr*" OR "less developed nation$"
    OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$"
    OR "underserved countr*" OR "underserved nation$"
    OR "deprived countr*" OR "deprived nation$"
    OR "middle income countr*" OR "middle income nation$"
    OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
    OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
    OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
    OR  "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "buginese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
    OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "essential" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kyrghizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"
    OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "maganese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish"
    )
)
```

## 4. Contributions

* v1.0.0: Eli Heldaas Seland (Oct 2021-Oct 2022)

* Internal reviews: Håkon Magne Bjerkan, Caroline S. Armitage (Jan 2022); Caroline S. Armitage, Marta Lorenz (March 2022)

Specialist input: Various academic staff from Western Norway University of Applied Sciences, including: A professor in Climate change, Sustainability and Education (Jan 2022); Workshops with 6 educational science academics (Feb 2022, Jun 2022).

## 5. Footnotes
<a id="f5"></a> Blanchard et al. (2017). *Words into action guidelines: National Disaster Risk Assessment. Special Topics: K. Consideration of Marginalized and Minority Groups in a National Disaster Risk Assessment*. United Nations Office for Disaster Risk Reduction. https://www.undrr.org/publication/marginalized-and-minority-groups-consideration-ndra. [↩](#Blanchard)

<a id="f4"></a> Brewer, L. (2013). *Enhancing youth employability: What? Why? and How? Guide to core work skills*. International Labour Office, Skills and Employability Department. https://www.ilo.org/wcmsp5/groups/public/@ed_emp/@ifp_skills/documents/publication/wcms_213452.pdf [↩](#iloskills)

<a id="f6"></a> Office of the High Commissioner (n.d.) *Non-discrimination: Groups in vulnerable situations. Special Rapporteur on the right to health*. United Nations Human Rights. https://www.ohchr.org/en/special-procedures/sr-health/non-discrimination-groups-vulnerable-situations (accessed Jun 2022). [↩](#UNOHC)

<a id="f9"></a> Pienaar, E., Grobler, L., Busgeeth, K., Eisinga, A. and Siegfried, N. (2011). *Developing a geographic search filter to identify randomised controlled trials in Africa: finding the optimal balance between sensitivity and precision*. Health Information & Libraries Journal, 28: 210-215. https://doi.org/10.1111/j.1471-1842.2011.00936.x. [↩](#Africancountries)

<a id="f1"></a> Statistics Division (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f3"></a> UNESCO (2012). *International Standard Classification of education ISCED 2011*. http://uis.unesco.org/en/topic/international-standard-classification-education-isced [↩](#isced)

<a id="f2"></a> UNESCO (n.d.a). *SDG Resources for Educators - Quality Education*. https://en.unesco.org/themes/education/sdgs/material/04 [accessed Jun 2022] [↩](#unescoquality)

<a id="f8"></a> UNESCO (n.d.b). *ESD for 2030 toolbox: Implementation*. https://en.unesco.org/themes/education-sustainable-development/toolbox/implementation#esd-impl-46 [accessed Jun 2022] [↩](#unescogced)

<a id="f11"></a> UNESCO Institute for Statistics. (2018). *Metadata for the global and thematic indicators for the follow-up of SDG 4 and Education 2030*. http://uis.unesco.org/sites/default/files/documents/metadata-global-thematic-indicators-sdg4-education2030-2017-en_1.pdf [↩](#unescotcg)

<a id="f10"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f7"></a> United Nations (n.d.) *Fight racism. Vulnerable groups, who are they?*. https://www.un.org/en/fight-racism/vulnerable-groups?gclid=EAIaIQobChMI9ODI_PvC9wIVV53VCh3pQgZCEAAYASAAEgInB_D_BwE (accessed Jun 2022). [↩](#UNracism)
