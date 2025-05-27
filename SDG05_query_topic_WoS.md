# Search query for SDG 05 - Gender equality, Bergen topic-approach.

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

This document contains search strings for finding publications related to the topics in the SDG 5 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in the SDG 5 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f3)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

## 3. Targets

### Target 5.1

> **5.1 End all forms of discrimination against all women and girls everywhere**
>
> 5.1.1 Whether or not legal frameworks are in place to promote, enforce and monitor equality and non‑discrimination on the basis of sex

This target is about 

```py
TS=
(

)
```

### Target 5.2

> **5.2 Eliminate all forms of violence against all women and girls in the public and private spheres, including trafficking and sexual and other types of exploitation**
>
> 5.2.1 Proportion of ever-partnered women and girls aged 15 years and older subjected to physical, sexual or psychological violence by a current or former intimate partner in the previous 12 months, by form of violence and by age
>
> 5.2.2 Proportion of women and girls aged 15 years and older subjected to sexual violence by persons other than an intimate partner in the previous 12 months, by age and place of occurrence

This target is about 

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

This target is about 

```py
TS=
(

)
```

### Target 5.4

> **5.4 Recognize and value unpaid care and domestic work through the provision of public services, infrastructure and social protection policies and the promotion of shared responsibility within the household and the family as nationally appropriate**
>
> 5.4.1 Proportion of time spent on unpaid domestic and care work, by sex, age and location

This target is interpreted to cover research about unpaid care and domestic work. This includes as related to public services, infrastructure, social protection policies, and the sharing of responsibility within households/families, but also more general aspects, such as effects and time spent (given the indicator). 

This target is interpreted to cover research about unpaid care and domestic work.

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

This query consists of 1 phrase. This phrase aims to find research about unpaid care and domestic work. The structure is _unpaid care and domestic work_.

_Unpaid care and domestic work_ can be challenging to isolate, as a) some unpaid domestic activities can also be done outside the home, b) some unpaid domestic activities can be paid labour, and d) some works often refer to unpaid work *without* using expressions for unpaid (e.g. "housework"). Therefore, the string is built up with various combinations "types of labour" with either terms for "unpaid", terms for "time use", or terms for "gender" or labour division, via trial and error. `time use surveys` do not exclusively collect data about unpaid labour, but they do include this and are about the home, thus help limiting to work about unpaid labour in the home when using more generic labour terms such as "maintenance". The phrase `division of labo$r` works in the same way, as it is often used to describe the division within a household (but not always, hence it is not used in all parts). Gender terms work in the same way - certain unpaid household activities are so gendered that this helps limit to them, however gender is also a prevalent theme in works about paid care activities. 

Firewood and water collection is included as a specific activity where women and girls tend to bear a high load. Here, `collected` is excluded as it tends to produce works where samples were collected, not the activity of firewood/water collection.  

Some activities are limited to being combined with unpaid terms: ´"household responsibil*" OR "domestic responsibilit*" OR "domestic work" OR "domestic labo$r" OR "domestic management"´ - this is to avoid the household responsitbility system (China), domestic labour in agriculture, and "domestic" as used to mean within the current country-

Firewood and water collection is included as a specific activity where women and girls tend to bear a high load. Here, `collected` is excluded as it tends to produce works where samples were collected, not the activity of firewood/water collection.  

```py
TS=
(
    "informal care" OR "informal caregiv*" OR "informal carer$" OR "reproductive labo$r" OR "kin work" OR "kinwork"
    OR "household management" OR "household administration"
    OR "housework" OR "household work" OR "household labo$r" OR "household task$" OR "household chore$" OR "household duties" 
    OR "domestic task$" OR "domestic chore$" OR "domestic duties" OR "domestic responsibilit*" 
    OR
    (("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data") 
    NEAR/15 ("care" OR "carer$" OR "household responsibil*" OR "domestic responsibilit*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home")
    )
    OR
    (
        ("unpaid" OR "without pay" OR "with no pay" OR "informal support" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "division of labo$r")
        AND 
            ("childcare" OR "caregiv*" OR "eldercare" OR "parenting"
            OR (("care" OR "carer$" OR "caring" ) NEAR/5 ("child*" OR "elderly" OR "disabled" OR "dependent$" OR "sick"))
            )
    )
    OR "domestic division of labo$r"
    OR
    (
        ("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "division of labo$r" OR "invisble labo$r")
        AND 
            ("cooking" OR "meal preparation" OR "food preparation" OR "cleaning" OR "washing" OR "repair" OR "maintenance" 
            OR "pay bills" OR "pet care" OR "shopping" OR "domestic management" OR "home management" OR "manage the home" 
            )
        AND ("household*" OR "domestic*" OR "home$" OR "family" OR "families" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
    )
    OR
    (
        ("unpaid" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
        AND
        (
            (("collection" OR "collecting" OR "fetch*") NEAR/5 ("fuel" OR "firewood" OR "drinking water" OR "well water" OR "clean water" OR "fetching water"))
            OR "household responsibil*" OR "domestic work" OR "domestic labo$r" OR "domestic management" OR "manage the home"
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

This target is about 

```py
TS=
(

)
```

### Target 5.6

> **5.6 Ensure universal access to sexual and reproductive health and reproductive rights as agreed in accordance with the Programme of Action of the International Conference on Population and Development and the Beijing Platform for Action and the outcome documents of their review conferences**
>
> 5.6.1 Proportion of women aged 15-49 years who make their own informed decisions regarding sexual relations, contraceptive use and reproductive health care
>
> 5.6.2 Number of countries with laws and regulations that guarantee full and equal access to women and men aged 15 years and older to sexual and reproductive health care, information and education

This target is about 

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
- Women's access and rights to financial services ("financial inclusion"). We interpret this as money-based resources. For this we include research about access to forms of microfinance, digital finance and mobile money, plus other more traditional financial products/financial services. Includes credit, savings, payment services, fund transfers and insurance.
- Women's access and rights to economic resources and land/property/inheritance/natural resources (including rights for tenure, ownership and control, and security). We interpret "economic resources" to include mentioned elements such as land and natural resources, but could also include human capital/labour (e.g. access to employment).

As in 1.4, we based this interpretation of financial and economic resources on <a href="#f2">UN DESA (2009, p1)</a>, which states:

> Economic resources refer to the direct factors of production such as “immoveable” assets, including land, housing, common pool resources and infrastructure, as well as “moveable” assets, such as productive equipment, technology and livestock. Financial resources refer to money-based resources, including government expenditures, private financial flows and official development assistance, as well as income, credit, savings and remittances. [...] Labour is the primary resource available to the vast majority of people, particularly those from low-income households [...]

#### Phrase 1

This phrase covers women's access and rights to financial services. The basic structure is access/rights + financial services + women.

Sources of terms for financial services included <a href="#f2">UN DESA (2009)</a> and a digital financial inclusion report from the <a href="#f3">UNSGSA et al. (2018)</a>. For the topic approach, we allow some terms which are already closely related to the idea of access to stand alone without being connected to access or rights explicitly; this includes microfinance types (where access is a primary objective) and "financial inclusion".

```py
TS=
(
    (
        ("financial inclusion" OR "microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance" OR "microcredit" OR "micro-credit" OR "microloan$" OR "micro-loan$")
        OR
        (
            ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
            OR "ownership" OR "control" OR "right$" OR "empower*" OR "inclusion"
            OR "affordab*" OR "pro poor" OR "inexpensive" OR "free of charge" OR "free service$"
            OR "inaccessib*" OR "barrier$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*" OR "exclusion"
            OR "unaffordab*" OR "expensive"
            OR "unbanked"
            )
            NEAR/15
            ("banks" OR "a bank" OR "banking" OR "bank account$"
            OR "digital finance" OR "mobile money" OR "electronic payments" OR "digital payment$" OR "fintech"
            OR "credit" OR "savings" OR "insurance" OR "payment service$" OR "transfer service$" OR "transfer funds"
            OR (("financial" OR "monetary") NEAR/1 ("resourc*" OR "opportunit*" OR "asset*" OR "servic*"))
            )
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

This phrase covers access and rights to economic resources, natural resources, land, property and inheritance. The basic structure is access/rights + resources + women.

"security" is used in phrases because otherwise there are many results about food security. Note: This string needs editing re issue [#173](https://github.com/SDGforskning/sdg-strings/issues/173)

```py
TS=
(
    (
        ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
        OR "ownership" OR "control" OR "right$"
        OR "affordab*" OR "pro poor"
        OR "empower*" OR "inclusion" OR "sharing"
        OR "tenure security" OR "secure tenure" OR "income security" OR "secure livelihood$"
        OR "inaccessib*" OR "barrier$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*"
        OR "unaffordab*" OR "exclusion" OR "land grab*" OR "insecurity"
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

This target is about 

```py
TS=
(

)
```

### Target 5.c

> **5.c Adopt and strengthen sound policies and enforceable legislation for the promotion of gender equality and the empowerment of all women and girls at all levels**
>
> 5.c.1 Proportion of countries with systems to track and make public allocations for gender equality and women’s empowerment

This target is about 

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

<span id="f2">UN DESA (2009).</span> *2009 World Survey on the Role of Women in Development: Women’s Control over Economic Resources and Access to Financial Resources, including Microfinance*. United Nations. https://www.un.org/womenwatch/daw/public/WorldSurvey2009.pdf

<span id="f3">UNSGSA</span> (Office of the United Nations Secretary-General’s Special Advocate for Inclusive Finance for Development, Her Majesty Queen Máxima of the Netherlands), the Better Than Cash Alliance, the United Nations Capital Development (UNCDF), and the World Bank. (2018).  *Igniting SDG Progress through Digital Financial Inclusion*. https://www.betterthancash.org/explore-resources/igniting-sdg-progress-through-digital-financial-inclusion [accessed 30.04.2022] 