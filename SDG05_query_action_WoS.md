# Search query for SDG 05 - Gender equality, Bergen action-approach.

Achieve gender equality and empower all women and girls

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the actions in the SDG 5 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 5 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f3)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

Acronyms used:
- UN DESA: UN Department of Economic and Social Affairs

## 3. Targets

### Target 5.1

> **5.1 End all forms of discrimination against all women and girls everywhere**
>
> 5.1.1 Whether or not legal frameworks are in place to promote, enforce and monitor equality and non‑discrimination on the basis of sex

This target is interpreted to cover research about:
- ending discrimination against women and girls
- strengthening and securing legal frameworks to promote, enforce and monitor equality and non-discrimination on the basis of sex

We use the definition of discrimination against women in Article 1 of the CEDAW Convention 
https://www.ohchr.org/sites/default/files/documents/publications/OHCHR-IPU-CEDAW-Handbook-revised-edition.pdf: "any distinction, exclusion or restriction made on the bases of sex which has the effect or purpose of impairing or nullifying the recognition, enjoyment or exercise by women, irrespective of their marital status, on a basis of equality of men and women, of human rights and fundamental freedoms in the political, economic, social, cultural, civil or any other field".

Sex/gender?


This query consist of x phrases. 

#### Phrase 1 

This phrase is about ending discrimination against women and girls. The general structure is action + discrimination + women & girls

```py
TS=
(
    (
        (
        ("decreas*" OR "minimi*" OR "reduc*" OR "mitigat*" 
        OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
        OR "end" OR "ending" OR "eliminat*" OR "eradicat*" OR "prevent*"
        OR "lift out of" OR "lifting out of" OR "overcom*" OR "escap*" OR "relief"
        )    
        NEAR/5
        (
         ("discriminat*" OR "exclusion" OR "dispar*" OR "bias*") OR
             (
                ("impair*" OR "nullif*" OR "violat*" OR "reduc*" OR "limit*")         
                NEAR/5
                ("human right*" OR "freedom*")
            )
        ) 
        NEAR/5 
        (*women" OR "*woman" OR "*womens" OR "*womans"
        OR "girl$" OR "female$" OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$"
        OR "pregnan*" OR "maternity" OR "maternal"
        OR "gender*" OR "transgender*")
        )
    ) 
)
```


#### Phrase 2

This phrase is about establishing, securing etc. legal frameworks concerning equality and non-discrimination on the basis of sex

```py
TS=
(
    (
        ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "more efficient" OR "higher" OR "upgrad*" OR "scal* up" OR "build*" OR "expand" OR "expansion*" OR
        "accelerat*" OR "advance" OR "advancing" OR "develop" OR "developing" OR "overcome" OR "ensure" OR "attain*" OR "achiev*" OR "establish*" OR "propose*" OR "design*" OR "implement*" OR "adopt*" OR "introduc*"
        ) 
        NEAR/5
        (
            ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance")
            NEAR/5
            (             
               ("equality*" OR "discriminat*" OR "exclusion" OR "dispar*" OR "bias*")
                NEAR/5 
                ("sex*" OR "gender*" OR "transgender*" OR "*women" OR "*woman" OR "*womens" OR "*womans" OR "girl$" OR "female$" OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "pregnan*")
            )
            
        )
    )
)
```


### Target 5.2

> **5.2 Eliminate all forms of violence against all women and girls in the public and private spheres, including trafficking and sexual and other types of exploitation**
>
> 5.2.1 Proportion of ever-partnered women and girls aged 15 years and older subjected to physical, sexual or psychological violence by a current or former intimate partner in the previous 12 months, by form of violence and by age
>
> 5.2.2 Proportion of women and girls aged 15 years and older subjected to sexual violence by persons other than an intimate partner in the previous 12 months, by age and place of occurrence

This target is interpreted to cover research about
* eliminating all forms of violence against women and girls in public and private spheres

Violence against women is defined by the UN as "any act of gender-based violence that results in, or is likely to result in, physical, sexual, or mental harm or suffering to women, including threats of such acts, coercion or arbitrary deprivation of liberty, whether occurring in public or in private life" <a href="#f2hb">(UN OHCHR, 1993)</a>


```py
TS=
(

)
```

### Target 5.3

> **5.3 Eliminate all harmful practices, such as child, early and forced marriage and female genital mutilation**
>
> 5.3.1 Proportion of women aged 20-24 years who were married or in a union before age 15 and before age 18
>
> 5.3.2 Proportion of girls and women aged 15-49 years who have undergone female genital mutilation/cutting, by age

This target is interpreted to cover research about
* eliminating all harmful practices against women and girls

Harmful practices are regarded as human rights violations and forms of violence, so there is overlap with target 5.2. Harmful practices only concerning boys or young men are considered irrelevant.

```py
TS=
(

)
```

### Target 5.4

> **5.4 Recognize and value unpaid care and domestic work through the provision of public services, infrastructure and social protection policies and the promotion of shared responsibility within the household and the family as nationally appropriate**
>
> 5.4.1 Proportion of time spent on unpaid domestic and care work, by sex, age and location

This target is interpreted to cover research about:
- Recognition and valuing unpaid care and domestic work, including work on caregiver burden and economic costs
- Provision of public services, infrastructure, and social protection policies in any way related to unpaid care and domestic work
- The promotion of shared responsibility for unpaid care and domestic work, including division and fairness. Although the SDG limits this to "within households and the family", in practice, it is difficult to separate the sharing of work within the household, and the sharing of work with e.g. professional services, and it being more equitable in other dimensions. Therefore we take a wider interpretation where we consider shared responsibility and division generally. 

We used two sources to help clarify what should fall under unpaid care and domestic work: The indicator metadata for target 5.4 (<a href="#f4ca">Statistics Division 2024</a>) and a report published by the UNDP Regional Bureau for Asia and the Pacific (<a href="#f6ca">Yamamoto 2018</a>). We include:
- Food and meals management and preparation
- Cleaning and maintenance of own dwelling and surroundings
- Do-it-yourself decoration
- Care, maintenance and repair of personal and household goods, textiles and footwear (e.g. washing clothes)
- Household management (e.g. paying bills, organising)
- Pet care
- Shopping for household and family members
- Collection of water and firewood/fuel
- Childcare and instruction
- Care of dependant adults, or non-dependant household or family members (e.g. sick, elderly or disabled )
- Travel or transporting goods related to these activities

Factors to do with valuation of this work, or services and policies mentioned in <a href="#f6ca">Yamamoto (2018)</a> include:
- the structure of social welfare, contributions into pensions via care work (e.g. child credit), or taxes and tax breaks (valuing)
- piped water, water sanitation/purification, irrigation and electricity/modern energy (public services/infrastructure)
- public investment in care services and care industry, such as childcare, preschool, personal care, elderly care, nursing homes, care facilities (public services), 
- parental leave (policies/shared responsibility)
- flexible work hours (policies/share responsibility)
- mobile banking and delivery of shopping (services)

_Unpaid care and domestic work_ can be challenging to isolate, as a) some unpaid domestic activities (e.g. caregiving, childcare) can be done outside the home or as paid/professional work, and b) some research may refer to unpaid work *without* using terms for unpaid (e.g. "housework"). Therefore, the _unpaid care and domestic work_ string is built up with some terms alone, and others in combination (direct terms for unpaid household work/care are used alone, while more ambiguous terms for work/care combined with terms for _unpaid_, _time use_, _gender_ or _labour division_). 

_Time use_, _gender_ or _labour division_ terms are not strictly equivalent to "unpaid work", but function to limit research to unpaid work in certain combinations, because the time-use, gendered or division aspect nearly always refers to unpaid parts of the labour. `time use surveys` do not exclusively collect data about unpaid labour, but include this and are about the home, thus help limiting to unpaid labour in the home when using more ambiguous labour terms (such as "maintenance"). The phrase `division of labo$r` works in the same way, as it is often used to describe the division within a household (but is also used in workplaces or colonial insect biology, so cannot be combined with e.g. "care" alone). Gender terms work in the same way - certain unpaid household activities are gendered, and therefore this helps limit to them; however gender is also a prevalent theme in works about paid care activities and therefore can't be used in all places. `sex` terms (as opposed to gender) did not seem to yield relevant results. 

Some specific labour terms which one might expect to suffice alone are combined with _unpaid_, _time use_, _gender_ or _labour division_: ´"household responsibil*" OR "domestic responsibilit*" OR "domestic work" OR "domestic labo$r" OR "domestic management"´ - this is to avoid the household responsitbility system (China), domestic labour in agriculture, and "domestic" as used to mean within the current country.

Firewood and water collection is included as a specific activity where women and girls tend to bear a high load. Here, `collected` is excluded as it tends to produce works where water samples were collected, not the activity of firewood/water collection.  

This query consists of 3 phrases.

#### Phrase 1

This phrase aims to find research about recognition and valuing unpaid care and domestic work. The structure is _recognising/valuing (action) + unpaid care and domestic work_.

```py
TS=
(
    ("valu*" OR "recogni*" OR "credit*" OR "respect*" OR "acknowledg*" OR "significance" OR "importance"
    OR "GDP" OR "care economy" OR "contribution" OR "contribute" OR "cost$" $OR "price"
    OR "caregiver burden" OR "zarit burden interview" OR "CarerQol" OR "qol" OR "quality of life"
    )
    NEAR/15
        (
            ("informal" NEAR/3 ("care" OR "caregiv*" OR "carer$"))
            OR "family caregiv*" OR "reproductive labo$r" OR "reproductive work" OR "kin work" OR "kinwork" OR "motherwork"
            OR "household management" OR "household administration"
            OR "housework" OR "household work" OR "household labo$r" OR "household task$" OR "household chore$" OR "household duties" 
            OR "domestic task$" OR "domestic chore$" OR "domestic duties" OR "domestic responsibilit*" 
            OR "domestic division of labo$r"
            OR
                (("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data") 
                NEAR/15 ("care" OR "carer$" OR "caring")
                )
            OR
            (
                ("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "informal support" OR "invisible labo$r" OR "division of labo$r")
                NEAR/15 
                    ("household responsibil*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home"
                    OR "childcare" OR "caregiv*" OR "eldercare" OR "parenting"
                    OR (("care" OR "carer$" OR "caring") NEAR/5 ("child*" OR "elderly" OR "disabled" OR "dependent$" OR "sick"))
                    OR
                        (
                            ("cooking" OR "meal preparation" OR "food preparation" OR "cleaning" OR "washing" OR "repair" OR "maintenance" 
                            OR "pay bills" OR "pet care" OR "shopping" OR "domestic management" OR "home management" OR "manage the home" 
                            )
                            NEAR/15 ("household*" OR "domestic*" OR "home$" OR "family" OR "families" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
                        )
                    )
            )
            OR
            (
                ("unpaid" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
                NEAR/15
                (
                    (("collection" OR "collecting" OR "fetch*") NEAR/5 ("fuel" OR "firewood" OR "drinking water" OR "well water" OR "clean water" OR "fetching water"))
                    OR "household responsibil*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home"
                ) 
            )
        )
)
```

#### Phrase 2

This phrase aims to find research about the provision of public services, infrastructure, and social protection policies in any way related to unpaid care and domestic work. The structure is _action + social services etc + unpaid care and domestic work_.

```py
TS=
(
    (
        ("provi*" OR "establish*" OR "offer*" OR "implement*" OR "plan" OR "adopt*" OR "introduc*" OR "reform*" 
        OR "increas*" OR "strengthen*" OR "improv*" OR "promot*" OR "enhanc*" OR "better" OR "scal* up" OR "build*" OR "expand" OR "expansion*" OR "develop" OR "developing"
        OR "policy" OR "policies" OR "law$" OR "regulat*" OR "legal*" OR "legislat*" OR "strateg*" OR "framework$" OR "instrument$"
        )
        NEAR/5
            ("social welfare" OR "welfare system$" OR "social protection" OR "social polic*"
            OR "tax break$" OR "tax credit$" OR "child credit$" OR "pension$"
            OR "public service$" OR "basic service$" OR "infrastructure" OR "modern energy" OR "irrigation" OR "electricity" OR "water sanitation" OR "clean water" OR "piped water" OR "water supply"
            OR "nursery" OR "daycare" OR "day care" OR "kindergarten" OR "preschool" 
            OR "elderly care" OR "nursing home$" OR "residential care" OR "care facilit*" OR "care service$" OR "home nurs*" OR "care home$" 
            OR (("formal" OR "professional") NEAR/3 ("care" OR "caregiv*"))
            OR "flexible work*" OR "flextime" OR "flexitime" OR "parental leave" OR "care* leave" OR "matern* leave" OR "patern* leave"
            )
    )
    NEAR/15
        (
            ("informal" NEAR/3 ("care" OR "caregiv*" OR "carer$"))
            OR "family caregiv*" OR "reproductive labo$r" OR "reproductive work" OR "kin work" OR "kinwork" OR "motherwork"
            OR "household management" OR "household administration"
            OR "housework" OR "household work" OR "household labo$r" OR "household task$" OR "household chore$" OR "household duties" 
            OR "domestic task$" OR "domestic chore$" OR "domestic duties" OR "domestic responsibilit*" 
            OR "domestic division of labo$r"
            OR
                (("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data") 
                NEAR/15 ("care" OR "carer$" OR "caring")
                )
            OR
            (
                ("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "informal support" OR "invisible labo$r" OR "division of labo$r")
                NEAR/15 
                    ("household responsibil*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home"
                    OR "childcare" OR "caregiv*" OR "eldercare" OR "parenting"
                    OR (("care" OR "carer$" OR "caring") NEAR/5 ("child*" OR "elderly" OR "disabled" OR "dependent$" OR "sick"))
                    OR
                        (
                            ("cooking" OR "meal preparation" OR "food preparation" OR "cleaning" OR "washing" OR "repair" OR "maintenance" 
                            OR "pay bills" OR "pet care" OR "shopping" OR "domestic management" OR "home management" OR "manage the home" 
                            )
                            NEAR/15 ("household*" OR "domestic*" OR "home$" OR "family" OR "families" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
                        )
                    )
            )
            OR
            (
                ("unpaid" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
                NEAR/15
                (
                    (("collection" OR "collecting" OR "fetch*") NEAR/5 ("fuel" OR "firewood" OR "drinking water" OR "well water" OR "clean water" OR "fetching water"))
                    OR "household responsibil*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home"
                ) 
            )
        )
)
```

#### Phrase 3

This phrase aims to find research about the promotion of shared responsibility for unpaid care and domestic work. The structure is _action + shared responsibility + unpaid care and domestic work_.

As the focus of the SDG is the gendered burden of this work, we also use some terms for gender to help find works about male participation in this labour. 

```py
TS=
(
    (
        ("provi*" OR "establish*" OR "offer*" OR "implement*" OR "plan" OR "adopt*" OR "introduc*" OR "reform*" 
        OR "increas*" OR "strengthen*" OR "improv*" OR "promot*" OR "enhanc*" OR "better" OR "scal* up" OR "build*" OR "expand" OR "expansion*" OR "develop" OR "developing"
        OR "reduc*" OR "decreas*" OR "prevent*" OR "hinder*" 
        OR "policy" OR "policies" OR "law$" OR "regulat*" OR "legal*" OR "legislat*" OR "strateg*" OR "framework$" OR "instrument$"
        )
        NEAR/5
            ("sharing" OR "shared" OR "share" OR "divide" OR "division" OR "fair*" OR "egalitarian" OR "equal*" OR "equitab*" OR "balanced" 
            OR "unequal*" OR "unfair*" OR "inequit*" OR "inequalit*"
            OR "male" OR "man" OR "men" OR "father*" OR "gender*"
            ) 
    )
    NEAR/15
        (
            ("informal" NEAR/3 ("care" OR "caregiv*" OR "carer$"))
            OR "family caregiv*" OR "reproductive labo$r" OR "reproductive work" OR "kin work" OR "kinwork" OR "motherwork"
            OR "household management" OR "household administration"
            OR "housework" OR "household work" OR "household labo$r" OR "household task$" OR "household chore$" OR "household duties" 
            OR "domestic task$" OR "domestic chore$" OR "domestic duties" OR "domestic responsibilit*" 
            OR "domestic division of labo$r"
            OR
                (("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data") 
                NEAR/15 ("care" OR "carer$" OR "caring")
                )
            OR
            (
                ("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "informal support" OR "invisible labo$r" OR "division of labo$r")
                NEAR/15 
                    ("household responsibil*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home"
                    OR "childcare" OR "caregiv*" OR "eldercare" OR "parenting"
                    OR (("care" OR "carer$" OR "caring") NEAR/5 ("child*" OR "elderly" OR "disabled" OR "dependent$" OR "sick"))
                    OR
                        (
                            ("cooking" OR "meal preparation" OR "food preparation" OR "cleaning" OR "washing" OR "repair" OR "maintenance" 
                            OR "pay bills" OR "pet care" OR "shopping" OR "domestic management" OR "home management" OR "manage the home" 
                            )
                            NEAR/15 ("household*" OR "domestic*" OR "home$" OR "family" OR "families" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
                        )
                    )
            )
            OR
            (
                ("unpaid" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
                NEAR/15
                (
                    (("collection" OR "collecting" OR "fetch*") NEAR/5 ("fuel" OR "firewood" OR "drinking water" OR "well water" OR "clean water" OR "fetching water"))
                    OR "household responsibil*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home"
                ) 
            )
        )
)
```

### Target 5.5

> **5.5 Ensure women’s full and effective participation and equal opportunities for leadership at all levels of decision-making in political, economic and public life**
>
> 5.5.1 Proportion of seats held by women in (a) national parliaments and (b) local governments
>
> 5.5.2 Proportion of women in managerial positions

This target is interpreted to cover research about: 
* Ensuring women's participation at all levels of decision-making in political, economic and public life 
* Ensuring women's equal opportunities for leadership at all levels of decision-making in political, economic and public life 
* Proportion of women in local and governmental bodies and in managerial positions

Private sphere (family and home life) not explicitly included in the search strings, but based on the Beijing Declaration (https://www.un.org/womenwatch/daw/beijing/pdf/Beijing%20full%20report%20E.pdf, including paragraph 185), we are aware that research on the private sphere may also be relevant.

Sources used for finding terms:  
 * UN Women, Key messages on women's rights: https://www.unwomen.org/sites/default/files/2024-06/in-brief-key-messages-on-womens-rights-empowerment-and-equality-electoral-and-political-participation-en.pdf 
 * Indicator metadata 5.5.2 https://unstats.un.org/sdgs/metadata/files/Metadata-05-05-02.pdf refers to ISCO-08, which lists useful terms to cover `managerial positions`: https://www.ilo.org/sites/default/files/wcmsp5/groups/public/%40dgreports/%40dcomm/%40publ/documents/publication/wcms_172572.pdf 
* Monitoring gender equality and the empowerment of women and girls in the 2030 agenda for sustainable development (Position paper), for terms about leadership positions: https://www.unwomen.org/sites/default/files/Headquarters/Attachments/Sections/Library/Publications/2015/IndicatorPaper-EN-FINAL.pdf 


This query consists of X phrases......

#### Phrase 1

The basic structure is _action_ + _women_ + _participation_ 
```py
TS=
(
    ("accelerat*" OR "achiev*" OR "advance" OR "advancing" OR "attain" OR "better" OR "boost*" OR "build" OR "develop*" OR "elevate" OR "elevating" OR "empower*" OR "enhanc*" OR "ensure"OR "expand" OR "expansion" OR "facilitat*" OR "foster*" OR "guarantee*" OR "heighten*" OR "higher*" OR "implement*" OR "improv*" OR "increas*" OR "promot*" OR "raise" OR "raising" OR "scal* up" OR "secur*" OR "strengthen*" OR "support")

    ("*women" OR "*woman" OR "*womens" OR "*womans"
    OR "girl$"
    OR "female$"
    OR "gender*"
    OR "transgender*"
    OR 
        ("sex*" 
        NEAR/5 ("based" OR "factor$" OR "distribution" OR "characteristic$" OR "dispar*" OR "difference*" OR "bias*" OR "discriminat*" OR "violence")
        )
    )


)
```

#### Phrase 2

The basic structure is _action_ + opposites/hindre diskriminering?
```py
TS=
(

)
```

#### Phrase 3

The basic structure is _action_ + _women_ + _leadership_ 

```py

```

#### Phrase 4

The basic structure is _action_ + _women_ + _proportion of seats/positions_ 

```py

```

### Target 5.6

> **5.6 Ensure universal access to sexual and reproductive health and reproductive rights as agreed in accordance with the Programme of Action of the International Conference on Population and Development and the Beijing Platform for Action and the outcome documents of their review conferences**
>
> 5.6.1 Proportion of women aged 15-49 years who make their own informed decisions regarding sexual relations, contraceptive use and reproductive health care
>
> 5.6.2 Number of countries with laws and regulations that guarantee full and equal access to women and men aged 15 years and older to sexual and reproductive health care, information and education

This target is interpreted to cover research about
* ensuring universal access to sexual and reproductive health and reproductive rights

The conferences mentioned in the target text relates to sexual and reproductive health in general, and with indicator 5.6.2 relating to both women and men, the interpretation of this target is not restricted to cover just women and girls. Topics and aspects of sexual and reproductive health is based on the mentioned conferences <a href="#f3hb">(ICPD, 1994) and </a> <a href="#f4hb">(UN Women, 2015)</a> and also related SDGs.

```py
TS=
(

)
```

### Target 5.a

> **5.a Undertake reforms to give women equal rights to economic resources, as well as access to ownership and control over land and other forms of property, financial services, inheritance and natural resources, in accordance with national laws**
>
> 5.a.1 (a) Proportion of total agricultural population with ownership or secure rights over agricultural land, by sex; and (b) share of women among owners or rights-bearers of agricultural land, by type of tenure
>
> 5.a.2 Proportion of countries where the legal framework (including customary law) guarantees women’s equal rights to land ownership and/or control

This target is essentially a subset of target 1.4 (SDG 1), where the focus is on women, and it does not include basic services or new technology:

> 1.4 By 2030, ensure that all men and women, in particular the poor and the vulnerable, have equal rights to economic resources, as well as access to basic services, ownership and control over land and other forms of property, inheritance, natural resources, appropriate new technology and financial services, including microfinance

We therefore interpret it in a similar way. We interpret 5.a to cover research about: 
- Ensuring women's access and rights to financial services ("financial inclusion"). We interpret this as money-based resources. For this we include research about access to forms of microfinance, digital finance and mobile money, plus other more traditional financial products/financial services. Includes credit, savings, payment services, fund transfers and insurance.
- Ensuring women's access and rights to economic resources and land/property/inheritance/natural resources (including rights for tenure, ownership and control, and security). We interpret "economic resources" to include mentioned elements such as land and natural resources, but could also include human capital/labour (e.g. access to employment).

As in 1.4, we based this interpretation of financial and economic resources on <a href="#f2ca">UN DESA (2009, p1)</a>, which states:

> Economic resources refer to the direct factors of production such as “immoveable” assets, including land, housing, common pool resources and infrastructure, as well as “moveable” assets, such as productive equipment, technology and livestock. Financial resources refer to money-based resources, including government expenditures, private financial flows and official development assistance, as well as income, credit, savings and remittances. [...] Labour is the primary resource available to the vast majority of people, particularly those from low-income households [...]

#### Phrase 1

This phrase covers ensuring women's access and rights to financial services. The basic structure is action + access/rights + financial services + women.

Sources of terms for financial services included <a href="#f2ca">UN DESA (2009)</a> and a digital financial inclusion report from the <a href="#f5ca">UNSGSA et al. (2018)</a>.

```py
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
                    OR "ownership" OR "control" OR "right$" OR "empower*" OR "inclusion"
                    OR "affordab*" OR "pro poor" OR "inexpensive" OR "free of charge" OR "free service$"
                    )
            )
            OR
            (
                ("reduce" OR "reducing" OR "decreas*" OR "avoid*" OR "prevent*" OR "combat*"
                OR "overcome" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "dismantl*"
                )
                NEAR/5
                    ("inaccessib*" OR "barrier$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*" OR "exclusion"
                    OR "unaffordab*" OR "expensive"
                    OR "unbanked"
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
        ("*women" OR "*woman" OR "*womens" OR "*womans"
        OR "girl$"
        OR "female$"
        OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$"
        OR "pregnan*" OR "maternity" OR "maternal" 
        OR "gender*"
        OR ("sex*" NEAR/5 ("based" OR "factor$" OR "distribution" OR "characteristic$" OR "dispar*" OR "difference*" OR "bias*" OR "discriminat*" OR "violence"))
        )
)
```

#### Phrase 2

This phrase covers ensuring access and rights to economic resources, natural resources, land, property and inheritance. The basic structure is action + access/rights + resources + women.

"security" is used in phrases because otherwise there are many results about food security. Note: This string needs editing re issue [#173](https://github.com/SDGforskning/sdg-strings/issues/173)

```py
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
                    OR "affordab*" OR "pro poor"
                    OR "empower*" OR "inclusion" OR "sharing"
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
        ("*women" OR "*woman" OR "*womens" OR "*womans"
        OR "girl$"
        OR "female$"
        OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$"
        OR "pregnan*" OR "maternity" OR "maternal" 
        OR "gender*"
        OR ("sex*" NEAR/5 ("based" OR "factor$" OR "distribution" OR "characteristic$" OR "dispar*" OR "difference*" OR "bias*" OR "discriminat*" OR "violence"))
        )
)
```

### Target 5.b

> **5.b Enhance the use of enabling technology, in particular information and communications technology, to promote the empowerment of women**
>
> 5.b.1 Proportion of individuals who own a mobile telephone, by sex


This target is interpreted to cover research about enhancing the use of enabling tecnology to promote empowerment of women. 

As both the target and the indicator emphasize ICT, we have an extra focus on ICT. However, all forms of enabling technologies may be included as relevant as long as they promote the empowerment of women.

United Nations' "Women’s Empowerment, SDGs and ICT", https://www.unapcict.org/sites/default/files/inline-files/Module_C1.pdf, defines ICT as: "ICT refers to all technology for creating, manipulating, storing, managing, sending and receiving information. ICT encompasses a wide range of multimedia and communication
tools. It can include, but is not limited to, old media such as radio, television and telephone,
as well as new media networks (fixed or wireless Internet), hardware (computers, mobile
phones, tablets, etc.) and software (social media services, multimedia applications, mobile apps, etc.)" (p. 31)

For definitions of gender equality and empowerment we use "Gender equality: Glossary of Terms and Concepts" from UNICEF: (https://www.unicef.org/rosa/media/1761/file/Genderglossarytermsandconcepts.pdf )

This query consists of 1? phrases......


#### Phrase 1

The basic structure is _action_ + _use_ + _technologies_ + _empowerment of women_

```py
TS=
(

)
```

#### Phrase 2

The basic structure is _action_ + 

```py
TS=
(

)
```

### Target 5.c

> **5.c Adopt and strengthen sound policies and enforceable legislation for the promotion of gender equality and the empowerment of all women and girls at all levels**
>
> 5.c.1 Proportion of countries with systems to track and make public allocations for gender equality and women’s empowerment

This target is interpreted to cover research about adopting and strengthening policies and legislation for the promotion of gender equality and for the empowerment of women and girls. According to Indicator metadata 5.c (https://unstats.un.org/sdgs/metadata/files/Metadata-05-0c-01.pdf ) we interpret the indicator to pertain to the characteristics of the financial system, not to the amount of funds each country spends on efforts for gender equality.

For definitions of _gender equality_ and _empowerment_ we use "Gender equality: Glossary of Terms and Concepts" from UNICEF: (https://www.unicef.org/rosa/media/1761/file/Genderglossarytermsandconcepts.pdf )

This query consists of X phrases......



## Phrase 1

The basic structure is _action_ + _policies/legislation_ + _gender equality/empowerment of women_  

```py
TS=
(

)
```
## Phrase 2

The basic structure is _systems for tracking/publishing allocations_  

```py
TS=
(

)
```
## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f1">UN DESA. (2025).</span> *Goals: Achieve gender equality and empower all women and girls*. https://sdgs.un.org/goals/goal5#targets_and_indicators [Accessed 2025.02.14]

<span id="f2hb">UN OHCHR. (1993).</span> *Declaration on the Elimination of Violence against Women*. https://www.ohchr.org/en/instruments-mechanisms/instruments/declaration-elimination-violence-against-women [Accessed 2025.05.08]

<span id="f3hb">ICPD. (1994).</span> *Programme of Action - Adopted at the International Conference on Population and Development (ICPD)*. https://www.unfpa.org/sites/default/files/event-pdf/PoA_en.pdf [Accessed 2025.05.08]

<span id="f4hb">UN Women. (2015).</span> *Beijing Declaration and Platform for Action, Beijing +5 Political Declaration and Outcome*. https://www.unwomen.org/en/digital-library/publications/2015/01/beijing-declaration[Accessed 2025.05.08]

<span id="f2ca">UN DESA (2009).</span> *2009 World Survey on the Role of Women in Development: Women’s Control over Economic Resources and Access to Financial Resources, including Microfinance*. United Nations. https://www.un.org/womenwatch/daw/public/WorldSurvey2009.pdf

<span id="f5ca">UNSGSA</span> (Office of the United Nations Secretary-General’s Special Advocate for Inclusive Finance for Development, Her Majesty Queen Máxima of the Netherlands), the Better Than Cash Alliance, the United Nations Capital Development (UNCDF), and the World Bank. (2018).  *Igniting SDG Progress through Digital Financial Inclusion*. https://www.betterthancash.org/explore-resources/igniting-sdg-progress-through-digital-financial-inclusion [accessed 30.04.2022] 

<span id="f4ca">Statistics Division</span> (2024). SDG Indicators Metadata Repository. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/metadata/ [accessed 22 May 2025]

<span id="f6ca">Yamamoto, Y</span> (2018). *Now is the Time! Reduce and redistribute the unpaid domestic and care work burden of women for sustainable development*. UNDP Asia and the Pacific.  https://www.undp.org/asia-pacific/publications/now-time-reduce-and-redistribute-unpaid-domestic-and-care-work-burden-women-sustainable-development [accessed 22 May 2025]
