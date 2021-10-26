# Search query for SDG 3 - Good health and well-being, Bergen action-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 3
3. Documentation and string sections for each target
4. Authorship and review
5. Footnotes


## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 3</summary>

```

```

</details>

## 2. General notes

Source of Targets and Indicators:
Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021]
<sup id="SDGT+Is">[1](#f1)</sup>

## 3. Targets

## Target 3.1/3.2

These targets are combined, as they cover similar topics.

> **3.1 By 2030, reduce the global maternal mortality ratio to less than 70 per 100,000 live births.**
>
> 3.1.1 Maternal mortality ratio
>
> 3.1.2 Proportion of births attended by skilled health personnel

> **2.2 3.2 By 2030, end preventable deaths of newborns and children under 5 years of age, with all countries aiming to reduce neonatal mortality to at least as low as 12 per 1,000 live births and under‑5 mortality to at least as low as 25 per 1,000 live births**
>
> 3.2.1 Under‑5 mortality rate
>
> 3.2.2 Neonatal mortality rate

The targets are interpreted as reducing the mortality rate for mothers during childbirth and for newborns and children under 5.
Children under five is however extremely difficult to limit bibliometrically since it is often referred to as childhood mortality - thus we include terms for children and infants generally.

This query consists of 2 phrases.

Both include a double `NOT` expression to help remove results referring to mortality of livestock, but retain those referring to these animals as models for humans.

##### Phrase 1:

The basic structure is *children/mothers* + *mortality* + *action* + *excluding livestock*

Having a wide `NEAR/15` interval helps to find results which talk reducing mortality via a factor: e.g. "xyz is a leading cause of maternal mortality. We examine how xyz can be prevented...."

`lower`, `limited` and `limits` are not included in the action terms due to general use (e.g. "limited understanding")

```Ceylon =
TS=
(
  (   ("child*" OR "infant$" OR "under-five"
      OR "fetus" OR "foetus" OR "fetal" OR "foetal" OR "perinatal" OR "prenatal" OR "neonatal" OR "antenatal" OR "newborn$"
      OR (("premature" OR "preterm") NEAR/3 ("birth$" OR "deliver*" OR "babies" OR "baby"))
      OR "maternal" OR "mothers" OR "childbirth" OR "child-birth" OR "birth"
      )
      NEAR/15
          ("mortality" OR "death$" OR "stillbirth$" OR "still-birth$")
      NEAR/15
          ("prevent*" OR "reduc*" OR "decreas*" OR "minimi*" OR "lowering" OR "lowered" OR "limit" OR "limiting" OR "combat*" OR "tackl*" OR "eliminat*" OR "avoid*")
  )
  NOT (("pigs" OR "cows" OR "sheep" OR "cattle") NOT ("human" OR "model"))    
)
```
##### Phrase 2:

Phrase 2 finds publications using the opposite terminology of phrase 1 (i.e. reduce mortality = increase survival). The basic structure is *children/mothers* + *survival* + *action* + *excluding livestock*.

```Ceylon =
TS=
(
  (   ("child*" OR "infant$" OR "under-five"
       OR "fetus" OR "foetus" OR "fetal" OR "foetal" OR "perinatal" OR "prenatal" OR "neonatal" OR "antenatal" OR "newborn$"
       OR (("premature" OR "preterm") NEAR/3 ("birth$" OR "deliver*" OR "babies" OR "baby"))
       OR "maternal" OR "mothers" OR "childbirth" OR "child-birth" OR "birth"
      )
      NEAR/15
          ("surviv*")
      NEAR/15
          ("improv*" OR "increas*" OR "enhanc*")
  )
  NOT (("pigs" OR "cows" OR "sheep" OR "cattle") NOT ("human" OR "model"))   
)
```
## Target 3.3

> **3.3 By 2030, end the epidemics of AIDS, tuberculosis, malaria and neglected tropical diseases and combat hepatitis, water-borne diseases and other communicable diseases.**
>
> 3.3.1 Number of new HIV infections per 1,000 uninfected population, by sex, age and key populations
>
> 3.3.2 Tuberculosis incidence per 100,000 population
>
> 3.3.3 Malaria incidence per 1,000 population
>
> 3.3.4 Hepatitis B incidence per 100,000 population
>
> 3.3.5 Number of people requiring interventions against neglected tropical diseases

The target is interpreted to include research which may help combat / end epidemics of communicable and waterborne diseases. Within "ending epidemics", we consider research on ending pandemics as relevant, along with general works about controlling spread/transmission. We interpret "combating" to mean reducing the occurrence and effects of these diseases, and thus include several approaches in addition to the generic action terms: treatment, prevention (e.g. vaccination) and drug development. We add these as many researchers may consider that it goes without saying that e.g. research on treatments for chagas are a form of "combating" chagas.

This query consists of 3 phrases. The basic structure for both is *communicable diseases* + *action*.

Action terms: `limited` was removed from the action terms, as it was used often in other contexts (e.g. "limited data"). Although `vaccination` may find some results on vaccine side effects, it also finds works on vaccination from a host of relevant perspectives (e.g. programs, barriers, hesitancy) - an alternative approach would be to add a near statement including all these terms.

##### Phrase 1

This covers communicable diseases as a category. The search terms here are difficult, as `communicable` will also find `non communicable` ("non communicable" seems to be the term causing the most problems; others, such as `non-infectious` seem to be used in papers about both, i.e. together with `infectious`). Non communicable diseases are covered in target 3.4, so in terms of SDG3 it is ok that they are included, but for a target-by-target approach it creates some noise. Approximately 10 % of the results for this phrase also include `non-communicable` (past 5 years). This is the reason these terms were split into a separate phrase.

``` Ceylon =
TS =
(
  ("communicable disease$" OR "communicable illness*")
  NEAR/15
      ("prevent*" OR "combat*" OR "fight*" OR "reduc*" OR "alleviat*" OR "treat*" OR "cure" OR "cured" OR "eradicat*" OR "eliminat*" OR "tackl*" OR "end" OR "ended" OR "ending"
      OR
        (
          ("stop" OR "stopped" OR "stopping" OR "limit" OR "limiting")
          NEAR/3 ("epidemic$" OR "pandemic$" OR "outbreak$" OR "spread" OR "transmission")
        )
      OR "vaccinate" OR "vaccination"
      OR (("develop*" OR "research*" OR "novel") NEAR/5 ("medicine$" OR "vaccine$" OR "cure" OR "drug$" OR "therap*"))
      )
)
```  

##### Phrase 2

The first section covers communicable and waterborne diseases as a category. See Phrase 1 for notes.

The second section covers specific communicable & vaccine-preventable diseases. `hepatitis`, `tuberculosis`, `HIV`, `malaria` are taken directly from the target. The term `AIDS` is not used as it is used as a verb. We then used the World Health Organization's (WHO) Global Health Observatory data repository for adding specific vaccine preventable & communicable diseases <sup id="WHOGHO">[2](#f2)</sup>. Here, they are listed according to SDG target; those under target 3.3. were included. This also included the category sexually transmitted infections.

The third section is for waterborne diseases. A definitive list of prioritised "waterborne diseases" was not found and the MeSH term has no specific diseases; as a way to improve the query, we have used 11 diseases/pathogens prioritised by the CDC Waterborne Diseases Prevention Branch <sup id="CDCwaterborne">[13](#f13)</sup>. I am unsure whether `diarrheal diseases` is too broad or not - waterborne pathogens are not the only cause, with WASH being a large factor. However, they may fall under "communicable" diseases more generally. Included so far.

The third section lists neglected tropical diseases, as mentioned in the target. The 20 diseases/disease groups currently prioritised by WHO in their 2021-2030 roadmap are included<sup id="WHONTD">[3](#f3)</sup>.

A number of these diseases also occur in animals (e.g. Feline/Simian Acquired Immunodeficiency Syndrome, Canine hepatitis, Avian malaria, Bovine tuberculosis). We do not attempt to exclude them, as it is considered that work on them can inform human prevention/treatment, or prevent zoonotic transmission.

Phrase 3 is the same as phrase 2, except it includes different action terms. These were separated out as they can be combined with `AND` rather than needing `NEAR`.


``` Ceylon =
TS =
(
  (
    (
      ("water borne" OR "waterborne" OR "water-borne" OR "water-related"
      OR "contagious" OR "transmissible" OR "infectious"
      )
      NEAR/5
          ("disease$" OR "infection$" OR "epidemic$" OR "illness*")
    )
    OR "hepatitis"
    OR "acquired immune deficiency syndrome" OR "acquired immuno-deficiency syndrome"  OR "acquired immunodeficiency syndrome" OR "Human Immunodeficiency Virus" OR "HIV"
    OR "tuberculosis"
    OR "malaria"
    OR "cholera"
    OR "meningitis"
    OR "influenza"
    OR "rubella"
    OR "diphtheria"
    OR "japanese encephalitis"
    OR "measles"
    OR "mumps"
    OR "tetanus"
    OR "pertussis"
    OR "polio*"
    OR "yellow fever"
    OR "sexually transmitted disease$" OR "sexually transmitted infection$"
    OR "syphilis"

    OR "amebiasis"
    OR "cryptosporidiosis" OR "cryptosporidium infection$"
    OR "giardiasis" OR "giardia infection$"
    OR "shigellosis"
    OR "cronobacter infection$"
    OR "acanthamoeba"
    OR "balamuthia"
    OR "naegleria"
    OR "sappinia"
    OR "typhoid"
    OR "diarrheal disease$"

    OR "neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthiases"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
  )
  NEAR/15
      ("prevent*" OR "combat*" OR "fight*" OR "reduc*" OR "alleviat*" OR "treat*" OR "cure" OR "cured" OR "eradicat*" OR "eliminat*" OR "tackl*" OR "end" OR "ended" OR "ending"
      )
)

```   

##### Phrase 3

Phrase 3 is the same as phrase 2, except it includes different action terms. These were separated out as they can be combined with `AND` rather than needing `NEAR`.

``` Ceylon =
TS =
(
  (
    (
      ("water borne" OR "waterborne" OR "water-borne" OR "water-related"
      OR "contagious" OR "transmissible" OR "infectious"
      )
      NEAR/5
          ("disease$" OR "infection$" OR "epidemic$" OR "illness*")
    )
    OR "hepatitis"
    OR "acquired immune deficiency syndrome" OR "acquired immuno-deficiency syndrome"  OR "acquired immunodeficiency syndrome" OR "Human Immunodeficiency Virus" OR "HIV"
    OR "tuberculosis"
    OR "malaria"
    OR "cholera"
    OR "meningitis"
    OR "influenza"
    OR "rubella"
    OR "diphtheria"
    OR "japanese encephalitis"
    OR "measles"
    OR "mumps"
    OR "tetanus"
    OR "pertussis"
    OR "polio*"
    OR "yellow fever"
    OR "sexually transmitted disease$" OR "sexually transmitted infection$"
    OR "syphilis"

    OR "amebiasis"
    OR "cryptosporidiosis" OR "cryptosporidium infection$"
    OR "giardiasis" OR "giardia infection$"
    OR "shigellosis"
    OR "cronobacter infection$"
    OR "acanthamoeba"
    OR "balamuthia"
    OR "naegleria"
    OR "sappinia"
    OR "typhoid"
    OR "diarrheal disease$"

    OR "neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthiases"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
  )
  AND
      (
        (
          ("prevent*" OR "combat*" OR "fight*" OR "reduc*" OR "treat*" OR "eradicat*" OR "eliminat*" OR "tackl*" OR "end" OR "ended" OR "ending" OR "stop" OR "stopped" OR "stopping" OR "limit" OR "limiting")
          NEAR/3
              ("epidemic$" OR "pandemic$" OR "outbreak$" OR "spread" OR "transmission")
        )
      OR "vaccinate" OR "vaccination"
      OR "antimalarial$" OR "antiviral$" OR "antibiotic$" OR "antiparasitic$" OR "antihelminthic$" OR "antihelmintic$"
      OR (("develop*" OR "research*" OR "novel") NEAR/5 ("medicine$" OR "vaccine$" OR "cure" OR "drug$" OR "therap*"))
      )
)

```   

## Target 3.4

> **3.4 By 2030, reduce by one third premature mortality from non-communicable diseases through prevention and treatment and promote mental health and well-being.**
>
> 3.4.1 Mortality rate attributed to cardiovascular disease, cancer, diabetes or chronic respiratory disease
>
> 3.4.2 Suicide mortality rate

This query consists of 3 phrases.
* Phrase 1 focuses on the "non-communicable diseases" part. It is interpreted to cover treatment, prevention and any other aspects related to reducing mortality. In contrast to 3.3, here there is an explicit focus on reducing mortality.
* Phrases 2 and 3 focus on the "mental health and well-being" part. It is interpreted to cover improving mental health, both by the treatment of disease and via health promotion.

##### Phrase 1:

We used World Health Organization factsheets to add the "main types" of non-communicable diseases<sup id="WHOFSnoncomm">[4](#f4)</sup>.

Cancer terms based on "The Cancer Dictionary" in the WHO Cancer Mortality Database <sup id="WHOcancer">[5](#f5)</sup> and using nomenclature as explained by the U.S. National Institutes of Health and National Cancer Institute SEER training modules <sup id="NIHcancer">[6](#f6)</sup>.

Premature death from these diseases can be covered within the phrasing of the action part (e.g. prevent premature mortality from noncommunicable diseases). Some action terms are stand-alone while others are combined with `mortality`; for `lower` this was necessary to avoid e.g. "cancer of the lower intestine".

``` Ceylon =
TS=
(
  (
    (
      ("non communicable" OR "noncommunicable" OR "non transmissible" OR "non infectious" OR "noninfectious")
      NEAR/5
          ("disease$" OR "illness*")
    )
    OR "cardiovascular disease$" OR "heart disease" OR "heart attack$" OR "stroke$"
    OR "diabetes"
    OR "chronic respiratory disease$" OR "asthma" OR "chronic obstructive pulmonary disease$" OR "COPD" OR "chronic obstructive airway disease$" OR "chronic bronchitis" OR "emphysema"
    OR "cancer$" OR "*sarcoma" OR "sarcoma$" OR "*carcinoma" OR "carcinoma$" OR "*blastoma" OR "blastoma$" OR "myeloma$" OR "lymphoma$" OR "leukaemia" OR "leukemia" OR "mesothelioma$" OR "melanoma$"  
    OR (("malignant" OR "incurable") NEAR/3 ("neoplasm$" OR "tumour$" OR "tumor$"))
  )
  NEAR/15
      ("prevent*" OR "combat*" OR "fight*" OR "reduc*" OR "alleviat*" OR "treat*" OR "cure" OR "cured" OR "eradicat*" OR "eliminat*" OR "tackl*"
      OR "cancer therapy" OR "cancer therapies"
      OR (("develop*" OR "research*" OR "novel") NEAR/5 ("medicine$" OR "vaccine$" OR "cure" OR "drug$" OR "therap*"))
      OR ("mortality" NEAR/3 ("decrease$" OR "lower"))
      OR ("survival" NEAR/3 ("improv*" OR "increas*" OR "enhanc*"))
      )
)

```  

##### Phrase 2:

This phrase focuses on non-communicable mental illnesses/diseases. The general structure is *disease* + *prevention/treatment*.

Generic categories and specific conditions are included. `suicid*` was mentioned specifically in the indicators. We used World Health Organization factsheets to add types of mental disorders<sup id="WHOFSmental">[7](#f7)</sup>. As the focus this phrase is illness, we did not consider developmental disorders to be relevant (e.g. autism).

``` Ceylon =
TS=
(
  ("mental health disorder$" OR "mental illness*"
  OR "suicid*"
  OR "depression" OR "depressive disorder$"
  OR "bipolar affective disorder"
  OR "schizophrenia"
  OR "psychosis" OR "psychoses"
  OR "dementia"
  )
  NEAR/15
      ("prevent*" OR "combat*" OR "fight*" OR "reduc*" OR "alleviat*" OR "eradicat*" OR "eliminat*" OR "tackl*"
      OR "intervention$" OR "treat*" OR "cure" OR "cured"
      OR (("develop*" OR "research*" OR "novel") NEAR/3 ("medicine$" OR "drug$"))
      OR ("decreas*" NEAR/3 ("occurrence" OR "incidence" OR "prevalence" OR "risk$" OR "rate$"))
      )
)
```

##### Phrase 3:

This phrase focuses on the promotion of well-being. The general structure is *well-being* + *promotion*.

`wellbeing` is used alone, rather than qualified with "mental" - well-being seems to be used to convey a sense of overall health, which should include the mental/psychosocial aspect. `quality of life` was tested, but this adds a lot of results which seem to be more medical (i.e.  quality of life could be improved after intervention x for condition y).

`increas*` was removed as an action term for `mental health` as it tends to be used in other ways (e.g. "increasing demand for services", "increasingly in focus")

``` Ceylon =
TS=
(
  ("mental health"
      NEAR/5 ("promote" OR "promotion" OR "strengthen*" OR "improv*" OR "intervention$")
  )
  OR
    (("well being" OR "wellbeing" OR "mental resilience" OR "psycho* resilience")
        NEAR/5 ("promote" OR "promotion" OR "strengthen*" OR "improv*" OR "increas*" OR "enhance*")
    )
)
```  

## Target 3.5

> **3.5 Strengthen the prevention and treatment of substance abuse, including narcotic drug abuse and harmful use of alcohol.**
>
> 3.5.1 Coverage of treatment interventions (pharmacological, psychosocial and rehabilitation and aftercare services) for substance use disorders
>
> 3.5.2 Alcohol per capita consumption (aged 15 years and older) within a calendar year in litres of pure alcohol

This target was interpreted to include research about the prevention and treatment of harmful uses of a) alcohol, and b) drugs/substances, rather than all use of alcohol/drugs.

This query consists of 1 phrase. The basic structure is *harmful use + prevention/treatment*.

Drug/substances were expanded using MeSH terms.
* Under "opioid-related disorders" (D000079524), `heroin`, `morphine`, `opiate` and `opium` are listed.
* Under "substance-related disorders" (D019966), a number of specific substances are listed, including `amphetamine`, `cocaine`, `inhalent`, `tobacco` etc.
`addiction` and `dependence` were considered as terms that can indicate harmful use.

`therapy` rather than `therap*` was used to prevent results regarding the therapeutic uses of these drugs/substances. The broad term `services` is used due to the variety of services involved (social, specialist, alcoholism, treatment, residential...).

``` Ceylon =
TS=
(
  ("binge drinking" OR "binge drinker$" OR "alcoholism"
    OR
    (
      ("drug$" OR "narcotic$" OR "narcotic$" OR "substance"
      OR "alcohol"
      OR "amphetamine$" OR "methamphetamine$" OR "MDMA" OR "ecstasy"
      OR "cocaine"
      OR "inhalant$" OR "amyl nitrite"
      OR "marijuana" OR "cannabis"
      OR "opioid$" OR "opiate$" OR "heroin" OR "morphine"
      OR "phencyclidine" OR "LSD" OR "psilocybin" OR "dimethyltriptamine"
      OR "khat"
      OR "tobacco"
      )
      NEAR/3
          ("abuse" OR "misuse" OR "harmful use*" OR "use disorder$" OR "dependence" OR "addict*" OR "overdose$")    
    )
  )
  NEAR/15
      ("prevent*" OR "combat*" OR "tackl*" OR "fight* against"
      OR "reduc*" OR "decreas*" OR "minimi*" OR "limit" OR "alleviat*"
      OR "treat*" OR "cure" OR "curing" OR "cured"
      OR "intervention$" OR "therapy" OR "therapies"
      OR "rehabilitat*" OR "aftercare" OR "services" OR "outreach"
      )
)
```

## Target 3.6

> **3.6 By 2020, halve the number of global deaths and injuries from road traffic accidents.**
>
> 3.6.1 Death rate due to road traffic injuries

This query consists of 2 phrases.

##### Phrase 1:

Note `limit$` not included (only `limiting`) as mostly used for city limits or speed limits.

``` Ceylon =
TS =
(
  (
    ("mortality" OR "death" OR "injury" OR "injuries" OR "accident$")
    NEAR/10
        ("traffic" OR "road" OR "motor-vehicle$")    
  )
  NEAR/5
      ("prevent*" OR "combat*" OR "reduc*" OR "decreas*" OR "minimi*" OR "lowering" OR "lowered" OR "limiting" OR "treat*" OR "avoid*")
)

```

##### Phrase 2:

`road` not included due to metaphorical use e.g. road to recovery.

``` Ceylon =
TS =
(
  (
    ("surviv*")
    NEAR/10
        ("traffic" OR "motor-vehicle$")    
  )
  NEAR/5
      ("improv*" OR "increas*" OR "enhanc*")
)

```

## Target 3.7 & 3.8

> **3.7 By 2030, ensure universal access to sexual and reproductive health-care services, including for family planning, information and education, and the integration of reproductive health into national strategies and programmes**
>
> 3.7.1 Proportion of women of reproductive age (aged 15–49 years) who have their need for family planning satisfied with modern methods
>
> 3.7.2 Adolescent birth rate (aged 10–14 years; aged 15–19 years) per 1,000 women in that age group

> **3.8 Achieve universal health coverage, including financial risk protection, access to quality essential health-care services and access to safe, effective, quality and affordable essential medicines and vaccines for all**
>
> 3.8.1 Coverage of essential health services
>
> 3.8.2 Proportion of population with large household expenditures on health as a share of total household expenditure or income

This query consists of 3 phrases.

##### Phrase 1:

``` Ceylon =
TS =
(
  ("health care" OR "health-care" OR "healthcare" OR "health service$" OR "medical service$" OR "medical care"
    OR "family planning"
    OR "medicine$" OR "vaccine$"
    OR
      (
        ("reproductive health" OR "sexual health" OR "mental health" OR "mental well-being" OR "psychiatric")
        NEAR/3
            ("support" OR "service$"
            OR "facility" OR "facilities" OR "hospital$" OR "clinic$"
            OR "treatment" OR "care"
            )      
      )
  )
  NEAR/5
      ("access*" OR "afford*" OR "barrier$")
)

```

##### Phrase 2:

We have included `health equity`. Definition from World Health Organisation: "Equity is the absence of avoidable, unfair, or remediable differences among groups of people, whether those groups are defined socially, economically, demographically or geographically or by other means of stratification. "Health equity” or “equity in health” implies that ideally everyone should have a fair opportunity to attain their full health potential and that no one should be disadvantaged from achieving this potential"<sup id="WHOequity">[8](#f8)</sup>.

``` Ceylon =
TS =
(
  "universal health coverage" OR "universal healthcare" OR "health equity"
)

```

##### Phrase 3:

``` Ceylon =
TS =
(
  ("reproductive health" OR "sexual health" OR "reproductive healthcare" OR "sexual healthcare")
  NEAR/10
      ("national" NEAR/3 ("program*" OR "strateg*" OR "policy" OR "policies"))
)

```

## Target 3.9

> **3.9 By 2030, substantially reduce the number of deaths and illnesses from hazardous chemicals and air, water and soil pollution and contamination**
>
> 3.9.1 Mortality rate attributed to household and ambient air pollution
>
> 3.9.2 Mortality rate attributed to unsafe water, unsafe sanitation and lack of hygiene (exposure to unsafe Water, Sanitation and Hygiene for All (WASH) services)
>
> 3.9.3 Mortality rate attributed to unintentional poisoning

This query consists of 2 phrases.

It is interpreted to mean pollution with chemicals/substances, or with pathogens that many contaminate water, air or soil.
* Whether food poisoning from contamination should be included is an open question - it is not air, soil or water per se, but does have to do with hygiene/sanitation (3.9.2). So far it is included. [Example result](https://www.webofscience.com/wos/woscc/full-record/WOS:A1993KR35200011)
* In Phrase 2, the inclusion of `sanitation` and terms for disease finds some results to do with sanitation and prevention of communicable disease - is this consistent? Does it fall under 3.9.2? Sanitation can refer to both infrastructure (relevant for preventing water contamination) but also personal sanitation. The same can be said for `hand hygiene`, `personal hygiene` etc. in Phrase 1.

##### Phrase 1:

The basic structure is *disease/mortality* + *pollutants/contamination* + *action*.

In the disease/mortality terms, only terms for mortality are included (not survival). For survival,  there are few results and they often concern animals.

To add specific types of air pollution, we used  World Health Organisation's (WHO) website about ambient air pollution<sup id="WHOairpoll">[9](#f9)</sup> and household air pollution <sup id="WHOhouseair">[10](#f10)</sup>. `air pollution` covers both ambient and indoor/household air pollution.

`poisoning*` was moved from the pollution terms (v2019-12) to the mortality terms, as it reflects a disease/mortality aspect already. This improves the results by finding those about carbon monoxide poisoning.

The combination of gases with `NEAR/15 "pollution" OR "poisoning$"` is necessary because there are medical papers that discuss these in terms of diagnosis or treatment (e.g. diffusion lung capacity of CO).

`hygiene` is not used alone as there are many results about oral hygiene which are probably too broad (not to do with pollution/contamination). `sanitation` is also broad, and can return animal results. Thus it is used as part of phrases below.


``` Ceylon =
TS =
(
  (
    ("mortality" OR "death$" OR "illness*" OR "disease$" OR "morbidity" OR "poisoning$")
    NEAR/10
        ( "air pollution" OR "PM2.5" OR "PM10" OR "fine particulate matter" OR "ground-level ozone"
          OR
            (
              ("nitrogen dioxide" OR "sulfur dioxide" OR "sulphur dioxide" OR "carbon monoxide" OR "volatile organic compounds")
              NEAR/15
                  ("pollution" OR "poisoning$")
            )
          OR "smoke pollution"
          OR "secondhand smok*" OR "second hand smok*" OR "involuntary smoking" OR "passive smoking"
          OR
            (
              ("drinking water" OR "potable water" OR "water source$" OR "sanitation")
              NEAR/3
                  ("unsafe" OR "safe" OR "contaminated" OR "contamination" OR "polluted" OR "clean" OR "sanitation")
            )
          OR "poor hygiene" OR "good hygiene" OR "hand hygiene" OR "personal hygiene" OR "hygiene practice$" OR "hygiene intervention$"
          OR "poor sanitation" OR "*adequate sanitation" OR "good sanitation" OR "sanitation facilities"
          OR
            (
              ("food" OR "foods")
              NEAR/3
                  ("unsafe" OR "contaminated" OR "contamination" OR "sanitation")
            )
        )

  )
  NEAR/15
      ( "prevent*" OR "combat*" OR "tackl*" OR "reduc*" OR "decreas*" OR "minimi*" OR "lowering" OR "lowered" OR "limiting" OR "limit" OR "eliminat*" OR "alleviat*" OR "avoid*"
        OR "treat*" OR "remov*" OR "clean up" OR "cleanup"
      )
)

```

##### Phrase 2:

The basic structure is *disease/mortality* + *pollutants/contamination* + *action* + *humans*.

This phrase was created as certain pollutants/contamination terms often give results for animals; thus they are combined with terms for humans. Certain diseases are also included in these terms for humans, because they are nearly always used in the context of humans and relevant for this topic.

World Health Organization's (WHO) website was used to add specific chemicals of major public health concern <sup id="WHOchem">[11](#f11)</sup>. For some reason `fluoride` was not included in v2019-12; now added. Inadequate fluoride is not included, as the target is focused on poisoning/contamination.

This string was simplified from v.2019-12 to remove the `NEAR/5 ("exposure" OR "residue$")` expression from the terms for chemicals of public health concern. The combination with terms for mortality and humans already implies exposure. A side-effect of this is that `lead` must be searched for as part of a phrase, due to its use as a verb.

`"poisoning$" OR "poisoned"` and `*toxicity` (covers gene/neuro/gonadotoxicity) were added to the mortality terms, as, in combination with the human terms, they are mostly used in the context of human illnesses. `fluorosis`, a disease from excess fluoride, was added.

The term `contamination` was used alone in v2019-12 - it is very broad. `contamination` is now limited to `water contamination` and `soil contamination` (+ variants). Contamination of food and drinking water is covered in phrase 1 (due to the lack of terms for humans, it is hard to search more generally there without introducing noise from biology).

This set was not limited to action terms in v2019-12. Now added, same as phrase 1.


``` Ceylon =
TS =
(
  (
    (
      ("mortality" OR "death$" OR "illness*" OR "disease$" OR "morbidity" OR "*toxicity" OR "poisoning$" OR "poisoned" OR "fluorosis")
      NEAR/10
          ("hazardous chemical$" OR "hazardous material$" OR "hazardous substance$" OR "pollution"
          OR "soil contamination" OR "contamination of soil$" OR "water contamination" OR "contamination of water"
          OR "arsenic" OR "asbestos" OR "benzene" OR "cadmium" OR "dioxin$" OR "mercury" OR "fluoride" OR "pesticide$"
          OR "lead poison*" OR "lead *toxicity" OR "lead mediated *toxicity" OR "lead induced *toxicity" OR "lead exposure" OR "lead carcinogen*" OR "blood lead"
          OR "sanitation"
          )
    )
    NEAR/15
        ("prevent*" OR "combat*" OR "tackl*" OR "reduc*" OR "decreas*" OR "minimi*" OR "lowering" OR "lowered" OR "limiting" OR "limit" OR "eliminat*" OR "alleviat*" OR "avoid*"
        OR "treat*" OR "remov*" OR "clean up" OR "cleanup"
        )
  )
  AND
      ("humans" OR "humanity" OR "human" OR "people" OR "person$"
        OR "children" OR "child" OR "infant$" OR "babies"
        OR "adult$" OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys"
        OR "rural" OR "urban" OR "city" OR "cities" OR "town$" OR "village$" OR "countr*" OR "nation$" OR "develop* state$"
        OR "patient$"
        OR "premature death$" OR "premature mortality"
        OR "neglected tropical disease$" OR "diarrhoea*" OR "diarrhea*"
      )
)

```

## Target 3.a

> **3.a Strengthen the implementation of the World Health Organization Framework Convention on Tobacco Control in all countries, as appropriate**
>
> 3.a.1 Age-standardized prevalence of current tobacco use among persons aged 15 years and older

This query consists of 1 phrase.

NB in the article version this was combined with 3.b, but no need, so here are split.

``` Ceylon =
TS =
(
  "World health organization framework convention on tobacco control"
)

```

## Target 3.b

> **3.b Support the research and development of vaccines and medicines for the communicable and non‑communicable diseases that primarily affect developing countries, provide access to affordable essential medicines and vaccines, in accordance with the Doha Declaration on the TRIPS Agreement and Public Health, which affirms the right of developing countries to use to the full the provisions in the Agreement on Trade-Related Aspects of Intellectual Property Rights regarding flexibilities to protect public health, and, in particular, provide access to medicines for all**
>
> 3.b.1 Proportion of the target population covered by all vaccines included in their national programme
>
> 3.b.2 Total net official development assistance to medical research and basic health sectors
>
> 3.b.3 Proportion of health facilities that have a core set of relevant essential medicines available and affordable on a sustainable basis

This query consists of 1 phrase.

Any works mentioning the DOHA declaration are likely to be addressing access to medicines

``` Ceylon =
TS =
(
  "DOHA declaration"
)

```

## Target 3.c

> **3.c Substantially increase health financing and the recruitment, development, training and retention of the health workforce in developing countries, especially in least developed countries and small island developing States**
>
> 3.c.1 Health worker density and distribution

This query consists of 1 phrase.

Types of healthcare worker expanded using MeSH terms.

Lists of least developed countries, small island developing states and landlocked developing states are from the United Nations World Economic Situation and Prospects (tables F, H and I, pages 173-174)<sup id="UNLDCs">[12](#f12)</sup>.

``` Ceylon =
TS =
(
  (
    (
      (  
         (
           ("health" OR "healthcare" OR "medical")
           NEAR/3
              ("workforce" OR "professional$" OR "worker$" OR "practitioner$" OR "human resources" OR "student$")
         )
         OR "nurse$" OR "doctor$" OR "physicians" OR "surgeons" OR "midwives" OR "gynecologists"
         OR "Anesthetists" OR "Audiologists" OR "Dental Staff" OR "Dentists" OR "Doulas" OR "Emergency Medical Dispatcher$" OR "Health Educators"
         OR "Health Facility Administrators" OR "Infection Control Practitioners" OR "Medical Chaperones" OR "Medical Laboratory Personnel"
         OR "Nutritionists" OR "Occupational Therapists" OR "Optometrists" OR "Pharmacists" OR "Physical Therapists" OR "Allergists" OR "Anesthesiologists"
         OR "Cardiologists" OR "Dermatologists" OR "Endocrinologists" OR "Gastroenterologists" OR "General Practitioners" OR "Geriatricians" OR "Hospitalists" OR "Nephrologists" OR "Neurologists"
         OR "Oncologists" OR "Ophthalmologists" OR "Otolaryngologists" OR "Pathologists" OR "Pediatricians" OR "Physiatrists" OR "Pulmonologists" OR "Radiologists" OR "Rheumatologists" OR "Urologists"
      )
      NEAR/10
          ("retention" OR "train" OR "training" OR "recruitment" OR "educat*" OR "professional development"
          OR "human capital flight" OR "brain drain" OR "emigration" OR "capacity building" OR "capacity development"
          OR "financing" OR "invest" OR "investment$" OR "investing"
          )
    )
    OR
    ( "health financing"
      OR
      (
        ("financing" OR "invest" OR "investment$" OR "investing")
        NEAR/3
            ("health service$" OR "healthcare" OR "medical care")
      )
    )    
  )
  AND
      (
        (("least developed" OR "least-developed" OR "developing") NEAR/2 ("countr*" OR "nation$" OR "state$"))
        OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
        OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands"
        OR "Afghanistan" OR "Armenia" OR "Azerbaijan" OR "Bhutan" OR "Bolivia" OR "Botswana" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "Ethiopia" OR "Kazakhstan" OR "Kyrgystan" OR "Lao People’s Democratic Republic" OR "Lesotho" OR "Malawi" OR "Mali" OR "Mongolia" OR "Nepal" OR "Niger" OR "Paraguay" OR "Republic of Moldova" OR "Rwanda" OR "South Sudan" OR "Tajikistan" OR "The former Yugoslav Republic of Macedonia" OR "Turkmenistan" OR "Uganda" OR "Uzbekistan" OR "Zambia" OR "Zimbabwe"        
      )
)

```

## Target 3.d

> **3.d Strengthen the capacity of all countries, in particular developing countries, for early warning, risk reduction and management of national and global health risks**
>
> 3.d.1 International Health Regulations (IHR) capacity and health emergency preparedness
>
> 3.d.2 Percentage of bloodstream infections due to selected antimicrobial-resistant organisms

This query consists of 1 phrase.

Health risks is a broad concept. We have interpreted it as sudden risks and disasters, given the concepts of "early warning" and "risk reduction" in the target.

The `NOT` statement is required to eliminate hits for e.g. crop epidemics.

``` Ceylon =
TS =
(
  (
    ("early warning*" OR "risk reduction" OR "management" OR "preparedness" OR "disaster planning")
    NEAR/5  
        ("health risk$" OR "pandemic$" OR "epidemic$" OR "medical disaster$" OR "health emergency" OR "health emergencies")
  )
  NOT
      ("blight" OR "plant pathogen$" OR "plant disease$")
)

```

## General SDG

`Secoisolariciresinol Diglucoside` is abbreviated to SDG, thus excluded.

``` Ceylon =
TS =
(
  ( "SDG$ 3" OR "SDG3" OR "SDG-3" OR "sustainable development goal$ 3"
    OR
    (
      ("sustainable development goal$" OR "SDG$" OR "goal 3")
      NEAR/15 "health"
    )
  )
  NOT "Secoisolariciresinol Diglucoside")
)

```

## 4. Authorship and review

## 5. Footnotes
<b id="f1">1</b> This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)".
(https://unstats.un.org/sdgs/indicators/indicators-list/) [↩](#SDGT+Is)

 <b id="f2">2</b> WHO (n.d.) Global Health Observatory data repository; By theme. http://apps.who.int/gho/data/node.home [accessed 15.10.2021]; WHO (n.d.) Global Health Observatory data repository; By category; Vaccine-preventable communicable diseases. http://apps.who.int/gho/data/node.main.170?lang=en [accessed 15.10.2021].[↩](#WHOGHO)

<b id="f3">3</b> p2 in World Health Organization. (2020). Ending the neglect to attain the Sustainable Development Goals: a road map for neglected tropical diseases 2021–2030. https://apps.who.int/iris/handle/10665/338565  [↩](#WHONTD)

<b id="f4">4</b> WHO (2018) Noncommunicable diseases. https://www.who.int/en/news-room/fact-sheets/detail/noncommunicable-diseases [accessed 15.11.2019] [↩](#WHOFSnoncomm)

<b id="f5">5</b> WHO, International Agency for Research on Cancer (2019) The Cancer Dictionary. http://www-dep.iarc.fr/WHOdb/WHOdb.htm [accessed 15.11.2019] [↩](#WHOcancer)

<b id="f6">6</b> NIH, NCI,SEER (n.d.) Cancer Classification. https://training.seer.cancer.gov/disease/categories/classification.html [accessed 15.11.2019] [↩](#NIHcancer)

<b id="f7">7</b> WHO (2019) Mental disorders. https://www.who.int/en/news-room/fact-sheets/detail/mental-disorders [accessed 29.11.2019] [↩](#WHOFSmental)

<b id="f8">8</b> WHO (n.d.) Health Equity. https://www.who.int/topics/health_equity/en/ [accessed 29.11.2019] [↩](#WHOequity)

<b id="f9">9</b> WHO (n.d.) Ambient air pollution: Pollutants. https://www.who.int/airpollution/ambient/pollutants/en/ [accessed 15.11.2019] [↩](#WHOairpoll)

<b id="f10">10</b> WHO (n.d.) Household air pollution: Pollutants. https://www.who.int/airpollution/household/pollutants/en/ [accessed 15.11.2019] [↩](#WHOhouseair)

<b id="f11">11</b> WHO (n.d.) International Programme on Chemical Safety, Ten chemicals of major public health concern. https://www.who.int/ipcs/assessment/public_health/chemicals_phc/en/ [accessed 15.11.2019]  [↩](#WHOchem)

<b id="f12">12</b> United Nations (2019) World Economic Situation and Prospects (Statistical Annex). https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<b id="f13">13</b> Centers for Disease Control and Prevention (2021) Waterborne Disease Prevention Branch. https://www.cdc.gov/ncezid/dfwed/waterborne/ [Accessed 15.10.2021] [↩](#CDCwaterborne)
