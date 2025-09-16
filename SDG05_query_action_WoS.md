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

Acronyms used:
- UN DESA: UN Department of Economic and Social Affairs

In many of the strings we use `"*womens" OR "*womans"` - this will also find results with "women's" and "woman's" in the current WOS search functionality. 

## 3. Targets

### Target 5.1

> **5.1 End all forms of discrimination against all women and girls everywhere**
>
> 5.1.1 Whether or not legal frameworks are in place to promote, enforce and monitor equality and non‑discrimination on the basis of sex

This target is interpreted to cover research about:
- ending discrimination and reducing inequality on the basis of sex and gender, including improving specifically women and girls' rights, freedoms, equality etc.
- strengthening and securing legal frameworks to promote, enforce and monitor equality and non-discrimination on the basis of sex and gender

While the target states "all women and girls", we use a wider gender and sex interpretation for two reasons. 1. Some research which is relevant to discrimination against women and girls uses gender-neutral terms such as "gender discrimination", and thus limiting to works mentioning women and girls might miss relevant works, 2. The indicator is on the basis of sex, not specifically about women and girls. 

For discrimination, we use the definition of discrimination against women in Article 1 of the CEDAW Convention 
https://www.ohchr.org/sites/default/files/documents/publications/OHCHR-IPU-CEDAW-Handbook-revised-edition.pdf: "any distinction, exclusion or restriction made on the bases of sex which has the effect or purpose of impairing or nullifying the recognition, enjoyment or exercise by women, irrespective of their marital status, on a basis of equality of men and women, of human rights and fundamental freedoms in the political, economic, social, cultural, civil or any other field".

**Working note**: It is possible that the terms `prejudice, misogyn*, sexism, sexist` will need to be discussed/removed. Pros/cons:
- Our reading of the CEDAW defines discrimination as action/result, while prejudice and stereotyping are attitudes/biases -> Remove
- The CEDAW  recognises that prejudice and stereotyping need to be eliminated as part of stopping discrimination, as outlined in Article 5 -> ?
- The other targets will not cover research about misogyny or sexism, making 5.1 the main option for including this research at all in SDG5 -> Keep
- Some terms are ambigous, for example "bias" can be an attitude and a result. Is it the same for "misogyny" (is hostility an attitude or an action)? https://www.ungei.org/gender-transformative-education-glossary/gender/misogyny -> ? 

This query consists of three phrases.

#### Phrase 1 

This phrase is about ending discrimination and reducing inequality regarding women/sex/gender. The general structure is *action + discrimination/rights + women/gender*

Removed `disparit* OR bias* OR difference*` from the women and gender string, as these find mostly medical papers regarding differences between the sexes in various health conditions.

```py
TS=
(
    ("decreas*" OR "minimi*" OR "reduc*" OR "mitigat*" 
    OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
    OR "end" OR "ending" OR "eliminat*" OR "eradicat*" OR "prevent*"
    OR "lift out of" OR "lifting out of" OR "overcom*" OR "escap*" OR "relief"
    )  
    NEAR/5
        ("misogyn*" OR "sexism" OR "sexist"
        OR
            (
                ("discriminat*" OR "dispar*"
                OR "prejudic*"
                OR "gender inequalit*" OR "gender inequit*" OR "gender bias*"
                OR (("bias*" OR "exclusion") NEAR/5 ("systematic*" OR "unconscious*"))
                OR
                    (
                        ("excludes" OR "exclude" OR "exclusion")
                        NEAR/2
                            ("*women" OR "*woman" OR "*womens" OR "*womans" OR "girl$" OR "female$" 
                            OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$" OR "wife" OR "wives" OR "girlfriend$" 
                            OR "gender*" OR "sexual and gender" OR "transgender*"
                            )
                    )
                OR "financial exclusion" OR "economic exclusion" OR "social exclusion" OR "digital exclusion" OR "cultural exclusion" OR "political exclusion"
                OR
                    ( 
                        ("impair*" OR "nullif*" OR "violat*" OR "reduc*" OR "limit*")         
                        NEAR/5 ("human right*" OR "women's right*" OR "freedom*" OR "right to" OR "rights")
                    )
                ) 
                NEAR/5 
                    ("*women" OR "*woman" OR "*womens" OR "*womans"
                    OR "girl$"
                    OR "female$"
                    OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
                    OR "wife" OR "wives" OR "girlfriend$"
                    OR "pregnan*" OR "maternity" OR "maternal"
                    OR "gender*" OR "sexual and gender" OR "transgender*"
                    OR ("sex" NEAR/5 ("based" OR "factor$" OR "distribution" OR "characteristic$" OR "discriminat*" OR "violence"))
                    )   
            )  
        )
)
```


#### Phrase 2 

This phrase aims to find works about improving inclusion, anti-discrimination, equality etc. (opposite of discrimination) regarding women/sex/gender. The general structure is *action + anti-discrimination/rights + women/gender*

```py
TS=
(
    ( "increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "more efficient*"
    OR "more effectiv*" OR "higher" OR "upgrad*" OR "scal* up" OR "build*" OR "expand" OR "expansion*"
    OR "accelerat*" OR "advance" OR "advancing" OR "develop" OR "developing" OR "encourag*" OR "facilitat*"
    OR "promot*" OR "raise" OR "raising" OR "raised" OR "foster*" OR "boost*" OR "overcome" OR "ensure" OR "attain*" OR "achiev*"
    )
    NEAR/5
        ("women's rights" OR "rights of women" OR "women's freedom"
        OR "women's inclusion" OR ("inclusion" NEAR/5 "gender")
        OR "gender equalit*" OR "gender equit*" OR "gender equal*"
        OR
            (
                ("human right*" OR "right to" OR "rights" OR "rights of" OR "anti-discriminat*" OR "non-discriminat*" OR "equalit*" OR "equal rights" 
                OR "financial inclusion" OR "economic inclusion" OR "social inclusion" OR "digital inclusion" OR "cultural inclusion" OR "policial inclusion"
                )
                NEAR/5
                    ("*women" OR "*woman" OR "*womens" OR "*womans"
                    OR "girl$"
                    OR "female$"
                    OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
                    OR "wife" OR "wives" OR "girlfriend$"
                    OR "pregnan*" OR "maternity" OR "maternal"
                    OR "gender*" OR "sexual and gender" OR "transgender*"
                    OR ("sex*" NEAR/5 ("based" OR "factor$" OR "distribution" OR "characteristic$" OR "dispar*" OR "difference*" OR "bias*" OR "discriminat*" OR "violence"))
                    )
            )
        )  
)
```


#### Phrase 3

This phrase is about establishing and improving legal frameworks/policies concerning equality and discrimination regarding women/gender/sex. The general structure is *action + legislation + equality + women/gender*

Removed `disparit* OR bias*` from the women and gender string, seems to cause issues in combination with `bias` and `strateg* OR regulat*` - many medical papers regarding e.g. sex-biased regulation of genes.

`strateg*` brings in a lot of results that are perhaps not really about legal frameworks (e.g. health strategies), and `regulation` brings in some about biological regulation - but difficult to remove?  

```py
TS=
(
    (
        (
            ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "more efficient"
            OR "higher" OR "upgrad*" OR "scal* up" OR "build*" OR "expand" OR "expansion*" OR "accelerat*" 
            OR "advance" OR "advancing" OR "develop" OR "developing" OR "overcome" OR "ensure" OR "attain*" 
            OR "achiev*" OR "establish*" OR "propose*" OR "design*" OR "implement*" OR "adopt*" OR "introduc*"
            ) 
            NEAR/5
                ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR
                "treaty" OR "treaties" OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "monitor*"
                )
        )
        NEAR/15
        (             
            ("exclusion" NEAR/5 "gender") OR ("inclusion" NEAR/5 "gender")
            OR "misogyn*" OR "sexism" OR "sexist"
            OR 
            (
                ("equality*" OR "discriminat*" OR "rights" OR "dispar*" OR "bias*" OR "opportunit*" OR "empower*"
                OR "financial exclusion" OR "financial inclusion" OR "economic exclusion" OR "economic inclusion" OR "social exclusion" OR "social inclusion" 
                OR "digital exclusion" OR "digital inclusion" OR "cultural inclusion" OR "cultural exclusion" OR "policial inclusion" OR "political exclusion"
                OR "*women's inclusion"
                )
                NEAR/5 
                    ("*women" OR "*woman" OR "*womens" OR "*womans"
                    OR "girl$"
                    OR "female$"
                    OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
                    OR "wife" OR "wives" OR "girlfriend$"
                    OR "pregnan*" OR "maternity" OR "maternal"
                    OR "gender*" OR "sexual and gender" OR "transgender*"
                    OR ("sex*" NEAR/5 ("based" OR "factor$" OR "distribution" OR "characteristic$" OR "difference*" OR "discriminat*" OR "violence"))
                    )
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

#### Phrase 1

This phrase is about ending violence against women and girls. The general structure is action + violence + women & girls

```py
TS=
(
	("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" 
	OR "limit$" OR "limiting" OR "limited" OR "mitigat*"
	OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" 
	OR "lower$" OR "lowered" OR "fight*" OR "combat" OR "combatting" 
	OR "declin*" OR "abate$" OR "abating" OR "diminish*"
	) 
	NEAR/10 
		("violence" OR "violent" OR "exploit*" OR "physical harm" OR "emotional harm" OR "harmful"
		) 
		NEAR/10
		    ("*women" OR "*woman" OR "*womens" OR "*womans"
                OR "girl$"
                OR "female$"
                OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
                OR "wife" OR "wives" OR "girlfriend$"
                OR "pregnan*" OR "maternity" OR "maternal"
                OR "gender*" OR "sexual and gender" OR "transgender*"
		    )
		
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

#### Phrase 1

This phrase is about eliminating harmful practices against women and girls. The general structure is action + practice + women & girls

```py
TS=
(
	("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" 
	OR "limit$" OR "limiting" OR "limited" OR "mitigat*"
	OR "degrad*" OR "tackl*" OR "alleviat*" OR "lowering" 
	OR "lower$" OR "lowered" OR "fight*" OR "combat" OR "combatting" 
	OR "declin*" OR "abate$" OR "abating" OR "diminish*"
	) 
	NEAR/10 
		("harmful practice$" OR "female genital mutilation" OR "FGM" "female genital cutting" OR "circumcision$" OR (("child" OR "children" OR "force*") NEAR/10 "marriage*")
        ) 
		NEAR
		    ("*women" OR "*woman" OR "*womens" OR "*womans"
                OR "girl$"
                OR "female$"
                OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
                OR "wife" OR "wives" OR "girlfriend$"
                OR "pregnan*" OR "maternity" OR "maternal"
                OR "gender*" OR "sexual and gender" OR "transgender*"
		    )
		
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

We used two sources to help clarify what should fall under unpaid care and domestic work: The indicator metadata for target 5.4 (<a href="#f4ca">Statistics Division 2024</a>) and a report published by the UNDP Regional Bureau for Asia and the Pacific (<a href="#f6ca">Yamamoto 2018</a>). We include food and meals management and preparation, cleaning and maintenance of own dwelling and surroundings, do-it-yourself decoration, care, maintenance and repair of personal and household goods, textiles and footwear (e.g. washing clothes), household management (e.g. paying bills, organising), pet care, shopping for household and family members, collection of water and firewood/fuel, childcare and instruction, care of dependant adults, or non-dependant household or family members (e.g. sick, elderly or disabled), travel or transporting goods related to these activities.

Factors to do with valuation of this work, or services and policies mentioned in <a href="#f6ca">Yamamoto (2018)</a> include:
- the structure of social welfare, contributions into pensions via care work (e.g. child credit), or taxes and tax breaks (valuing)
- piped water, water sanitation/purification, irrigation and electricity/modern energy (public services/infrastructure)
- public investment in care services and care industry, such as childcare, preschool, personal care, elderly care, nursing homes, care facilities (public services), 
- parental leave (policies/shared responsibility)
- flexible work hours (policies/share responsibility)
- mobile banking and delivery of shopping (services)

_Unpaid care and domestic work_ can be challenging to isolate, as a) some unpaid domestic activities (e.g. caregiving, childcare) can be done outside the home or as paid/professional work, and b) some research may refer to unpaid work *without* using terms for unpaid (e.g. "housework"). Therefore, the _unpaid care and domestic work_ string is built up with some terms alone, and others in combination (direct terms for unpaid household work/care are used alone, while more ambiguous terms for work/care combined with terms for _unpaid_, _time use_, _gender_ or _labour division_). 

_Time use_, _gender_ or _labour division_ terms are not strictly equivalent to "unpaid work", but function to limit research to unpaid work in certain combinations, because the time-use, gendered or division aspect nearly always refers to unpaid parts of the labour. `time use surveys` do not exclusively collect data about unpaid labour, but include this and are about the home, thus help limiting to unpaid labour in the home when using more ambiguous labour terms (such as "maintenance"). The phrase `division of labo$r` works in the same way, as it is often used to describe the division within a household (but is also used in workplaces or colonial insect biology, so cannot be combined with e.g. "care" alone). Gender terms work in the same way - certain unpaid household activities are gendered, and therefore this helps limit to them; however gender is also a prevalent theme in works about paid care activities and therefore can't be used in all places. `sex` terms (as opposed to gender) did not seem to yield many or relevant results. 

Some specific labour terms which one might expect to suffice alone are combined with _unpaid_, _time use_, _gender_ or _labour division_: ´"household responsibil*" OR "domestic responsibilit*" OR "domestic work" OR "domestic labo$r" OR "domestic management"´ - this is to avoid the household responsitbility system (China), domestic labour in agriculture, and "domestic" as used to mean within the current country.

Firewood and water collection is included as a specific activity where women and girls tend to bear a high load. Here, `collected` is excluded as it tends to produce works where water samples were collected, not the activity of firewood/water collection.  

Using `NEAR` for "formal/informal" care is important, as many works specify the type of care (e.g. "informal dementia care").

This query consists of 3 phrases. The _unpaid care and domestic work_ part of each phrase is identical. 

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
                (("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR ("gender*" NEAR/3 "division")) 
                NEAR/15 ("care" OR "carer$" OR "caring")
                )
            OR
            (
                ("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "informal support" OR "invisible" OR "division of" OR ("gender*" NEAR/3 "division"))
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
                ("unpaid" OR "invisible" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
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
            OR "tax break$" OR "tax credit$" OR "child credit$" OR "pension$" OR "caregiver benefit$"
            OR 
                (("income support" OR "financial support" OR "economic support" OR "cash" OR "allowance" OR "payment$" OR "subsid*" OR "leave") 
                NEAR/3 ("caregiv*" OR "care" OR "carer$" OR "childcare" OR "eldercare")
                )
            OR "nursery" OR "daycare" OR "day care" OR "kindergarten" OR "preschool" 
            OR "elderly care" OR "nursing home$" OR "residential care" OR "care facilit*" OR "care service$" OR "home nurs*" OR "care home$" 
            OR (("formal" OR "professional") NEAR/3 ("care" OR "caregiv*"))
            OR "flexible work*" OR "flextime" OR "flexitime" OR "parental leave" OR "matern* leave" OR "patern* leave"
            OR "public service$" OR "basic service$" OR "infrastructure" OR "modern energy" OR "electricity" 
            OR "irrigation" OR "water sanitation" OR "clean water" OR "piped water" OR "water supply"
            OR "mobile bank*" OR "mobile financ*" OR "delivery service$" 
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
                (("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR ("gender*" NEAR/3 "division")) 
                NEAR/15 ("care" OR "carer$" OR "caring")
                )
            OR
            (
                ("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "informal support" OR "invisible" OR "division of" OR ("gender*" NEAR/3 "division"))
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
                ("unpaid" OR "invisible" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
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
                (("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR ("gender*" NEAR/3 "division")) 
                NEAR/15 ("care" OR "carer$" OR "caring")
                )
            OR
            (
                ("unpaid" OR "without pay" OR "with no pay" OR "time use survey*" OR "time use statistic*" OR "time use data" OR "informal support" OR "invisible" OR "division of" OR ("gender*" NEAR/3 "division"))
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
                ("unpaid" OR "invisible" OR "women*" OR "woman" OR "girl$" OR "mother*" OR "gender*")
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
_From the review meeting 13.06.25: "Maybe consider only including the 3rd bullet of the interpretation in the topic approach? As it is more topic-y, and adding in an action ourselves (not defined in the target) is a bit dubious."_

Private sphere (family and home life) not explicitly included in the search strings, but based on the Beijing Report <a href="#f1li">(UN, 1995)</a>, including paragraph 185), we are aware that research on the private sphere may also be relevant.


Sources used for finding terms:  

* Indicator metadata 5.5.2 <a href="#f2li">(UN Statistics Division, 2025)</a> refers to ISCO-08, which lists useful terms to cover _managerial positions_ <a href="#f5li">(ILO, 2012)</a>.
* Monitoring Gender Equality and the Empowerment of Women and Girls in the 2030 Agenda for Sustainable Development <a href="#f3li">(UN Women, 2015)</a>, for terms about leadership positions.

This query consists of 3 phrases:

#### Phrase 1

The basic structure is _action_ + _women_ + _participation/leadership_ + _decisionmaking_

```py

TS= 
(
    (
        ("accelerat*" OR "achiev*" OR "adopt" OR "advance" OR "advancing" OR "attain*" OR "better" OR "build" 
        OR "develop*" OR "elevat*" OR "elevating" OR "empower*" OR "encourag*" OR "enhanc*" OR "ensur*" OR "expand" 
        OR "expansion" OR "establish*" OR "facilitat*" OR "foster*" OR "framework$" OR "guarantee*" OR "heighten*" 
        OR "higher*" OR "implement*" OR "improv*" OR "increas*" OR "initiative$" OR "introduc*" OR "law$" OR "legislat*" 
        OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "program" OR "programs" OR "promot*" OR "propos*" 
        OR "raise" OR "raising" OR "scal* up" OR "secur*" OR "strengthen*" OR "support"
        )
        NEAR/5    
            (
                (
                    ("female$" OR "*women" OR "*woman" OR "*womens" OR "*womans") 
                    OR (("gender*" OR "transgender*") NEAR/5 ("parit*" OR "equal*" OR "equi*" OR "balanc*"))
                )
                NEAR/5 
                    ("participat*" OR "involve*" OR "represent*" OR "engage*" OR "position*" OR "voice*" 
                    OR "vote" OR "votes" OR "voting" OR "leadership" OR "leader*" OR "head" OR "manager*" 
                    OR "management" OR "legislator*" OR "judge*" OR "minister*" OR "mp" OR "mps" 
                    OR "member of parliament" OR "government" OR "mayor*" OR "quota" 
                    OR
                        (
                            ("chief*" OR "senior" OR "top" OR "managing" OR "enterprise*" OR "board") 
                            NEAR/5 ("director*" OR "executive*" OR "officer*" OR "official*" OR "position*" OR "member*" OR "traditional")
                        )   
                    )
            )
    )
    AND
        ("decisionmak*" OR "decision-mak*" OR "policymak*" OR "policy-mak*" OR "politics"
        OR (("decision*" OR "decid*") NEAR/5 ("process*" OR "authorit*" OR "business*" OR "corporate" OR "public" OR "economic" OR "civil" OR "society" OR "communit*"))
        )
)

```

#### Phrase 2

The basic structure is the opposite of phrase 1: _remove barriers_ + _women_ + _participation/leadership_ + _(decisionmaking?)_

```py
TS=
(
    (
        ("alleviat*" OR "avoid*" OR "combat*" OR "counteract" OR "decreas*" OR "dismantl*" OR "eliminat*" OR "end" 
        OR "ends" OR "ended" OR "ending" OR "eradicat*" OR "fight*" OR "limit$" OR "limited" OR "limiting" 
        OR "minimi*" OR "mitigat*" OR "overcom*" OR "prevent*" OR "reduc*" OR "remov*" OR "stop*"
        )
        NEAR/3
        (
            (
                (
                    ("barrier*" OR "bias*" OR "discriminat*" OR "divide*" OR "exclusion" OR "hindrance*" OR "hinder" 
                    OR "inequal*" OR "unequal*" OR "inequit*" OR "unequit*" OR "obstacle*" OR "unbalanc*" 
                    OR "imbalance*" OR "disparit*" OR "underrepresentation"
                    )
                    NEAR/5
                        ("female$" OR "*woman" OR "*women" OR "*womens" OR "*womans*" 
                        OR (("gender*" OR "transgender*") NEAR/5 ("parit*" OR "equal*" OR "equit*" OR "balanc*"))
                        )  
                )
                OR "glass ceiling*" OR "gender divide*" OR "gender gap*" OR "gender disparity" OR "gender inequality" 
                OR "gender imbalance " OR "gender inequity"
            )
            NEAR/5 
                ("participat*" OR "involve*" OR "represent*" OR "engage*" OR "position*" OR "voice*" 
                OR "vote" OR "votes" OR "voting" OR "leadership" OR "leader*" OR "head" OR "manager*" 
                OR "management" OR "legislator*" OR "judge*" OR "minister*" OR "mp" OR "mps" 
                OR "member of parliament" OR "government" OR "mayor*" OR "quota" 
                OR 
                    (
                        ("chief*" OR "senior" OR "top" OR "managing" OR "enterprise*" OR "board") 
                        NEAR/5 ("director*" OR "executive*" OR "officer*" OR "official*" OR "position*" OR "member*" OR "traditional")
                    )
                )
        )
    )
    AND
        ("decisionmak*" OR "decision-mak*" OR "policymak*" OR "policy-mak*" OR "politics"
        OR (("decision*" OR "decid*") NEAR/5 ("process*" OR "authorit*" OR "business*" OR "corporate" OR "public" OR "economic" OR "civil" OR "society" OR "communit*"))
        )
)

```

### Target 5.6

> **5.6 Ensure universal access to sexual and reproductive health and reproductive rights as agreed in accordance with the Programme of Action of the International Conference on Population and Development and the Beijing Platform for Action and the outcome documents of their review conferences**
>
> 5.6.1 Proportion of women aged 15-49 years who make their own informed decisions regarding sexual relations, contraceptive use and reproductive health care
>
> 5.6.2 Number of countries with laws and regulations that guarantee full and equal access to women and men aged 15 years and older to sexual and reproductive health care, information and education

This target is interpreted to cover research about
* ensuring universal access to sexual and reproductive health
* ensuring universal access to reproductive rights

The conferences mentioned in the target text relates to sexual and reproductive health in general, and with indicator 5.6.2 relating to both women and men, the interpretation of this target is not restricted to cover just women and girls. Topics and aspects of sexual and reproductive health is based on the mentioned conferences <a href="#f3hb">(ICPD, 1994) and </a> <a href="#f4hb">(UN Women, 2015)</a> and also related SDGs.

#### Phrase 1
This phrase covers ensuring sexual and reproductive health as mentioned in the conference documents. The structure is action + health issue

```py
TS=
(
    ("accelerat*" OR "achiev*" OR "advance" OR "advancing" 
    OR "attain" OR "better" OR "boost*" OR "build" OR "develop*" 
    OR "elevate" OR "elevating" OR "empower*" OR "enhanc*" 
    OR "ensure"OR "expand" OR "expansion" OR "facilitat*" 
    OR "foster*" OR "guarantee*" OR "heighten*" OR "higher*" 
    OR "implement*" OR "improv*" OR "increas*" OR "promot*" 
    OR "raise" OR "raising" OR "scal* up" OR "secur*" OR "strengthen*" OR "support"
    )
    NEAR/10
        ("sexual health" OR "reproductive health" OR "safe pregnan*" OR "safe child birth$"
        )
)
```
#### Phrase 2
This phrase covers ensuring access and removing barriers for reproductive rights. The structure is action + access + reproductive rights

```py
TS=
(
    ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "higher"
    OR "overcome" OR "ensure" OR "attain*" OR "achiev*"OR "upgrad*"
    OR "scal* up" OR "expand" OR "expansion*" OR "advance" OR "advancing" OR "develop" OR "developing"
    OR 
        (
            ("decreas*" OR "minimi*" OR "reduc*" OR "limit$" OR "limiting" OR "limited" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*")
            NEAR/5 ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*")
        )
    OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*"
    )
    NEAR
        ("reproductive rights"
        )
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
                OR "improv*" OR "increase" OR "increasing" OR "increased" OR "better" OR "reform*"
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
                    ("inaccessib*" OR "barrier$" OR "hindrance$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*" OR "exclusion"
                    OR "unaffordab*" OR "expensive"
                    OR "unbanked"
                    )      
            )
        )
        NEAR/15
            ("microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance" OR "microcredit" OR "micro-credit" OR "microloan$" OR "micro-loan$"
            OR "banks" OR "a bank" OR "banking" OR "bank account$"
            OR "digital finance" OR "mobile money" OR "electronic payments" OR "digital payment$" OR "fintech"
            OR "credit" OR "entrepreneurial finance" OR "loan$" OR "savings" OR "insurance" OR "payment service$" OR "transfer service$" OR "transfer funds"
            OR (("financial" OR "monetary") NEAR/1 ("resourc*" OR "opportunit*" OR "asset*" OR "servic*"))
            OR "financial inclusion" 
            )
    )
    AND
        ("*women" OR "*woman" OR "*womens" OR "*womans"
        OR "girl$"
        OR "female$"
        OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
        OR "wife" OR "wives" OR "girlfriend$"
        OR "pregnan*" OR "maternity" OR "maternal" 
        OR "gender*"
        OR ("sex*" NEAR/5 ("based" OR "factor$" OR "distribution" OR "characteristic$" OR "dispar*" OR "difference*" OR "bias*" OR "discriminat*" OR "violence"))
        )
)
```

#### Phrase 2

This phrase covers ensuring access and rights to economic resources, natural resources, land, property and inheritance. The basic structure is action + access/rights + resources + women.

"security" is used in phrases because otherwise there are many results about food security. "control" is also used in phrases as it was found to cause too much noise alone (works mentioning "control groups" or "asthma control" for example). `("of" NEAR/1 "assets")` is used to help filter out many works from business (e.g. return on assets).

```py
TS=
(
    (
        (
            (
                ("ensure" OR "establish*" OR "propose*" OR "implement*"
                OR "improv*" OR "increase" OR "increasing" OR "increased" OR "better" OR "reform*"
                OR "adopt*" OR "introduc*" OR "build*" OR "plan" OR "planning" OR "plans"
                OR "develop" OR "attain*" OR  "achiev*" OR "improv*" OR "strengthen*" OR "increas*"
                OR "program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "initiative$" OR "law$" OR "legislat*"
                )
                NEAR/5
                    ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
                    OR "ownership" OR "landownership" OR "right$"
                    OR "control over" OR "control of" OR "control and use" OR "access and control" OR "individual control" OR "collective control" OR "territorial control" OR "land control" OR "economic control"
                    OR "affordab*" OR "pro poor"
                    OR "empower*" OR "inclusion" OR "sharing"
                    OR "tenure security" OR "secure tenure" OR "land tenure" OR "income security" OR "secure livelihood$"
                    )
            )
            OR
            (
                ("reduce" OR "reducing" OR "decreas*" OR "avoid*" OR "prevent*" OR "combat*"
                OR "overcome" OR "stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "remov*" OR "eliminat*" OR "eradicat*" OR "dismantl*"
                )
                NEAR/5
                    ("inaccessib*" OR "barrier$" OR "hindrance$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*"
                    OR "unaffordab*" OR "exclusion" OR "land grab*" OR "appropriation of land" OR "insecurity"
                    )      
            )
        )
        NEAR/5
            ("economic resource$" OR "employment" OR "decent work" OR "paid work" OR "labour market$"
            OR "income" OR "livelihood$" OR "wealth" OR "inheritance" OR "inherit" OR ("of" NEAR/1 "assets")
            OR "land" OR "lands" OR "landowner*" OR "farmland$" OR "property" OR "natural resource$" OR "tenure"
            )
    )
    AND
        ("*women" OR "*woman" OR "*womens" OR "*womans"
        OR "girl$"
        OR "female$"
        OR "sister$" OR "mother$" OR "aunt" OR "aunts" OR "grandmother$" OR "grandma$" OR "niece$" OR "daughter$"
        OR "wife" OR "wives" OR "girlfriend$"
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

"Women’s Empowerment, SDGs and ICT" from UN APCICT defines ICT as: "ICT refers to all technology for creating, manipulating, storing, managing, sending and receiving information. ICT encompasses a wide range of multimedia and communication
tools. It can include, but is not limited to, old media such as radio, television and telephone,
as well as new media networks (fixed or wireless Internet), hardware (computers, mobile
phones, tablets, etc.) and software (social media services, multimedia applications, mobile apps, etc.)" <a href="#f4li">(UN APCICT, 2016, p.31)</a>. 

For definitions of gender equality and empowerment we use "Gender equality: Glossary of Terms and Concepts" from UNICEF <a href="#f5li">(UNICEF, 2017)</a>. 


This query consists of 2 phrases.


#### Phrase 1

The basic structure is _action_ + _use of technology_ + _empowerment of women_

```py
TS=
(
    (
        ("accelera*" OR "achiev*" OR "adopt*" OR "advance" OR "advancing" OR  "attain*" OR "better" OR "build*" 
        OR "develop*" OR "consolidat*" OR "elevat*" OR "empower*" OR "encourag*" OR "enhanc*" OR "ensur*" 
        OR "establish*" OR "expand" OR "expansion"  OR "facilitat*" OR "foster*" OR "framework$" 
        OR "guarantee*" OR "heighten*" OR "higher" OR "implement*" OR "improv*" OR "increas*" OR "initiative$" 
        OR "introduc*" OR "law$" OR "legislat*" OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" 
        OR "program" OR "programs" OR "promot*" OR "propos*" OR "raise" OR "raising" 
        OR "scal* up" OR "secur*" OR "strateg*" OR "strengthen*" OR "support*"
        )
        NEAR/5
            (
                ("use" OR "usage" OR "utilization" OR "access" OR "adoption" OR "diffusion" OR "skills") 
                NEAR/5
                    ("enabling technolog*" OR "computer*" OR "digital" OR "handheld" OR "hardware" OR "ICTs" OR "ICT" OR "ICT4D" 
                    OR "information communications technolog*" OR "information technolog*" OR "innovative technolog*" OR "internet"
                    OR "ipad*" OR "iphone*" OR "laptop*" OR "mobile*" OR "multimedia" OR "online" OR "smartphone*" OR "social media"
                    OR "tablet*" OR "tehcnological intervention*" OR "telecommunication" OR "telehealth" OR "telephone*" 
                    OR "television" OR "web-based" OR "wi-fi" OR "wireless" OR "world wide web" 
                    )
            )
    )
    NEAR/15
        (
            ("female$" OR "*woman" OR "*women" OR "*womens" OR "*womans" OR 
            (("gender*" OR "transgender")  NEAR/5 ("parit*" OR "equal*" OR "equit*" OR "balanc*"))
            )
            NEAR/15    
                ("autonomy" OR "capacity*" OR "choice*" OR "control" OR "decision-making" OR "economic strength" 
                OR "emancipat*" OR "*empower*" OR "independence"  OR "personal priorities" OR "personal strength" 
                OR "political strength" OR "power" OR "self concept" OR "self confidence" OR "self efficacy"
                )
       )
)

```

#### Phrase 2

The basic structure is _action_ + _barriers_ + _use of technology_ + _empowerment of women_

```py
TS=
(
    (
        ("address*" OR "alleviat*" OR "avoid*" OR "combat*" OR "counteract*"  OR "decreas*" OR "dismantl*" 
        OR "eliminat*" OR "end" OR "ends" OR "ended" OR "ending" OR  "eradicat*" OR "fight*" OR "limit$" 
        OR "limited" OR "limiting" OR "manag*" OR "minimi*" OR "mitigat*" OR "overcom*" OR "reduc*" 
        OR "prevent*" OR "remov*" OR "stop*" OR "tackl*"   
        )
        NEAR/5
            ("barrier$" OR "discriminat*" OR "disempower*" OR "disparit*" OR "divide*" OR "hinder" OR "hindranc*" 
            OR "imbalance" OR "inequit*" OR "inequal*"  OR "obstacle*"  OR "unequit*" OR "unbalanc*" OR "unequal*" 
            )
    )
    NEAR/5
        (
            (
                ("use" OR "usage" OR "utilization" OR "access" OR "adoption" OR "diffusion" OR "skills") 
                NEAR/5
                    ("enabling technolog*" OR "computer*" OR "digital" OR "handheld" OR "hardware" OR "ICTs" OR "ICT" OR "ICT4D" 
                    OR "information communications technolog*" OR "information technolog*" OR "innovative technolog*" OR "internet"
                    OR "ipad*" OR "iphone*" OR "laptop*" OR "mobile*" OR "multimedia" OR "online" OR "smartphone*" OR "social media"
                    OR "tablet*" OR "tehcnological intervention*" OR "telecommunication" OR "telehealth" OR "telephone*" 
                    OR "television" OR "web-based" OR "wi-fi" OR "wireless" OR "world wide web"
                    )
            )
            NEAR/15
                ("female$" OR "*woman" OR "*women" OR "*womens" OR "*womans" 
                OR (("gender*" OR "transgender")  NEAR/5 ("parit*" OR "equal*" OR "equit*" OR "balanc*" OR "diversity"))
                )
            NEAR/15    
                ("autonomy" OR "capacity*" OR "choice*" OR "control" OR "decision-making" OR "economic strength" OR "emancipat*"
                OR "*empower*" OR "freedom" OR "independence" OR "personal priorities" OR "personal strength" 
                OR "political strength" OR "power" OR "self concept" OR "self confidence" OR "self efficacy"
                )
        )
)
```

### Target 5.c

> **5.c Adopt and strengthen sound policies and enforceable legislation for the promotion of gender equality and the empowerment of all women and girls at all levels**
>
> 5.c.1 Proportion of countries with systems to track and make public allocations for gender equality and women’s empowerment

This target is interpreted to cover research about policies and legislation for the promotion of gender equality and for the empowerment of women and girls. According to Indicator metadata 5.c <a href="#f6li">(UN Statistics, 2023)</a>    we interpret the indicator to pertain to the characteristics of the financial system, not to the amount of funds each country spends on efforts for gender equality.

For definitions of _gender equality_ and _empowerment_ we use "Gender equality: Glossary of Terms and Concepts" from UNICEF <a href="#f5li">(UNICEF, 2017)</a>.   


This query consists of 2 phrases:



## Phrase 1

The basic structure is _action (strengthen)_ + _policies/legislation_ + _gender (in)equality/empowerment of women_  

```py
TS=
(
    ("accelera*" OR "accept*" OR "achiev*" OR "adopt" OR "advance$" OR "advancing" OR "agree*" OR "architect*" 
    OR "attain*" OR "better" OR "build*" OR "confirm*" OR "consolidat*" OR "design*" OR "develop$" OR "developing" 
    OR "development" OR "elevat*" OR "empower*" OR "encourag*" OR "enhance" OR "ensur*" OR "establish*" 
    OR "expan$" OR "expansion*" OR "facilitat*" OR "foster*" OR "framework$" OR "guarantee*" OR "heighten*" 
    OR "higher" OR "implement*" OR "improv*" OR "increas*" OR "initiative$" OR "introduc*" OR "law$" 
    OR "legislat*" OR "maintain*" OR "more efficient" OR "pass" OR "plan" OR "plans" OR "planned" 
    OR "planning" OR "policy" OR "policies" OR "program" OR "programs" OR "promot*" OR "propos*" 
    OR "provid*" OR "raise" OR "raising" OR "reform$" OR "reforming" OR "reformed" OR "restor*" OR "scal* up" 
    OR "secur*" OR "strateg*" OR "strengthen"  OR "support*" OR "sustain$" OR "sustaining" OR "upgrad*"
    )  
    NEAR/3
        (
            ("action*" OR "agreement$" OR "framework$" OR "governance" OR "initiative$" OR "instrument$" 
            OR "law$" OR "legal*" OR "legislat*" OR "plan"  OR "policy" OR "policies" OR "practice$" 
            OR "principle$" OR "procedure*" OR "program*" OR "regulat*" OR "right*" OR "rule" 
            OR "rules" OR "strateg*" OR "treaty" OR "treaties"
            ) 
            NEAR/5
                ("GEWE"
                OR 
                    (
                        ("gender*" OR "transgender*")  
                        NEAR/3 
                            ("parit*" OR "disparit*" OR "equal*" OR "inequal*" 
                            OR "unequal*" OR "equit*" OR "inequit*" OR "unequit*" OR "balanc*" OR "imbalanc*" 
                            OR "unbalanc*" OR "discriminat*" OR "diversity" OR "gap" OR "divide*" OR "bias"
                            )
                    )
                OR
                    (
                        ("female$" OR "*woman" OR "*women" OR "*womens" OR "*womans" OR "girl$") 
                        NEAR/3 
                            ("autonomy" OR "capacity*" OR "choice*" OR "control" OR "decision-making" OR "economic strength" 
                            OR "emancipat*" OR "*empower*" OR "freedom" OR "independence"  OR "personal priorities" 
                            OR "personal strength" OR "political strength" OR "power" OR "right*" OR "self concept" 
                            OR "self confidence" OR "self efficacy"
                            )
                    )
                )
        )
)
```
## Phrase 2

The basic structure is _action (decrease)_ + _discriminatory policies/legislation_  

```py
TS=
( 
    ("alleviat*" OR "combat*" OR "decreas*" OR "eliminat*" OR "end" OR "ending" OR "eradicat*" 
    OR "fight*" OR "minimi*" OR "mitigat*" OR "overcom*" OR "prevent*" 
    OR "reduc*" OR "remov*" 
    )     
    NEAR/5
        (
            ("agreement$" OR "framework$" OR "governance" OR "law$" OR "legal*" OR "legislat*" OR "plan"  
            OR "policy" OR "policies" OR "principle$" OR "procedure*" OR  "regulat*" OR "right*" OR "rule" OR "rules" OR "strateg*" OR "treaty" OR "treaties"
            ) 
            NEAR/5
                (
                    ("bias*" OR "discriminat*" OR "dispar*" OR "parit*" OR "gap" OR "exclud*" OR "exclusion" 
                    OR "impair*" OR   "violat*" OR "equal*" OR "inequal*" OR "unequal*" OR "equit*" OR "inequit*"
                    OR "unequit*" OR "balanc*" OR "imbalanc*"   OR "unbalanc*" OR "diversity" OR "gap" OR "divide*"
                    )
                    NEAR/3 ("female$" OR "*woman" OR "*women" OR "*womens" OR "*womans" OR "girl$" OR "gender" OR "transgender*")
                )
        )
)

```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f3hb">ICPD. (1994).</span> *Programme of Action - Adopted at the International Conference on Population and Development (ICPD)*. https://www.unfpa.org/sites/default/files/event-pdf/PoA_en.pdf [Accessed 2025.05.08]

<span id="f5li">ILO. (2012).</span> *International Standard Classification of Occupations: Structure, group definitions and correspondence tables: ISCO–08, Volume I*. https://www.ilo.org/sites/default/files/wcmsp5/groups/public/%40dgreports/%40dcomm/%40publ/documents/publication/wcms_172572.pdf [Accessed 2025.06.12]

<span id="f1li">UN. (1995).</span> *Report of the Fourth World
Conference on Women*. https://www.un.org/womenwatch/daw/beijing/pdf/Beijing%20full%20report%20E.pdf [Accessed 2025.06.05]

<span id="f4li">UN APCICT. (2016).</span> *Women’s Empowerment, SDGs and ICT*.  https://www.unapcict.org/sites/default/files/inline-files/Module_C1.pdf [Accessed 2025.06.05]

<span id="f2ca">UN DESA (2009).</span> *2009 World Survey on the Role of Women in Development: Women’s Control over Economic Resources and Access to Financial Resources, including Microfinance*. United Nations. https://www.un.org/womenwatch/daw/public/WorldSurvey2009.pdf

<span id="f1">UN DESA. (2025).</span> *Goals: Achieve gender equality and empower all women and girls*. https://sdgs.un.org/goals/goal5#targets_and_indicators [Accessed 2025.02.14]

<span id="f2hb">UN OHCHR. (1993).</span> *Declaration on the Elimination of Violence against Women*. https://www.ohchr.org/en/instruments-mechanisms/instruments/declaration-elimination-violence-against-women [Accessed 2025.05.08]

<span id="f5ca">UNSGSA</span> (Office of the United Nations Secretary-General’s Special Advocate for Inclusive Finance for Development, Her Majesty Queen Máxima of the Netherlands), the Better Than Cash Alliance, the United Nations Capital Development (UNCDF), and the World Bank. (2018).  *Igniting SDG Progress through Digital Financial Inclusion*. https://www.betterthancash.org/explore-resources/igniting-sdg-progress-through-digital-financial-inclusion [accessed 30.04.2022] 

<span id="f6li">UN Statistics Division. (2023).</span> *SDG indicator metadata*. [5.c.1] https://unstats.un.org/sdgs/metadata/files/Metadata-05-0c-01.pdf [Accessed 2025.06.05]

<span id="f2li">UN Statistics Division. (2025).</span> *SDG indicator metadata*. [5.5.1] https://unstats.un.org/sdgs/metadata/files/Metadata-05-05-02.pdf [Accessed 2025.06.05]

<span id="f4hb">UN Women. (2015).</span> *Beijing Declaration and Platform for Action, Beijing +5 Political Declaration and Outcome*. https://www.unwomen.org/en/digital-library/publications/2015/01/beijing-declaration[Accessed 2025.05.08]

<span id="f3li">UN Women. (2015).</span> *Monitoring Gender Equality and the Empowerment of women and girls in the 2030 Agenda for Sustainable Development: Opportunities and Challenges: Position Paper*. https://www.unwomen.org/sites/default/files/Headquarters/Attachments/Sections/Library/Publications/2015/IndicatorPaper-EN-FINAL.pdf    [Accessed 2025.06.05]

<span id="f7li">UNICEF. (2017).</span> *Gender Equality: Glossary of Terms and Concepts*. https://www.unicef.org/rosa/media/1761/file/Genderglossarytermsandconcepts.pdf [Accessed 2025.06.05]

<span id="f6ca">Yamamoto, Y</span> (2018). *Now is the Time! Reduce and redistribute the unpaid domestic and care work burden of women for sustainable development*. UNDP Asia and the Pacific.  https://www.undp.org/asia-pacific/publications/now-time-reduce-and-redistribute-unpaid-domestic-and-care-work-burden-women-sustainable-development [accessed 22 May 2025]