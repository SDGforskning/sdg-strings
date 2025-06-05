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

This target is about 

```py
TS=
(

)
```

### Target 5.5

> **5.5 Ensure women’s full and effective participation and equal opportunities for leadership at all levels of decision-making in political, economic and public life**
>
> 5.5.1 Proportion of seats held by women in (a) national parliaments and (b) local governments
>
> 5.5.2 Proportion of women in managerial positions

This target is interpreted to cover research about: 
* Women's participation at all levels of decision-making in political, economic and public life 
* Women's equal opportunities for leadership at all levels of decision-making in political, economic and public life 
* Proportion of women in local and governmental bodies and in managerial positions

Private sphere (family and home life) not explicitly included in the search strings, but based on the Beijing Report <a href="#f1li">(UN, 1995)</a>, including paragraph 185), we are aware that research on the private sphere may also be relevant.

Sources used for finding terms:  
  * Indicator metadata 5.5.2 <a href="#f2li">(xxx, 20xx)</a> https://unstats.un.org/sdgs/metadata/files/Metadata-05-05-02.pdf refers to ISCO-08, which lists useful terms to cover `managerial positions`: https://www.ilo.org/sites/default/files/wcmsp5/groups/public/%40dgreports/%40dcomm/%40publ/documents/publication/wcms_172572.pdf 
* Monitoring Gender Equality and the Empowerment of Women and Girls in the 2030 Agenda for Sustainable Development <a href="#f3li">(UN Women, 2015)</a>, for terms about leadership positions



This query consists of X phrases......

## Phrase 1

The basic structure is _women_ + _participation_ 

```py
TS=
(

)
```
## Phrase 2

The basic structure is _ opposites/hindre diskriminering_ + ?
```py
TS=
(

)
```

## Phrase 3
The basic structure is _women_ + _leadership_ 
```py

```
## Phrase 4
The basic structure is _women_ + _proportion of seats/positions_ 
```py


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

This target is about 

```py
TS=
(

)
```

### Target 5.b

> **5.b Enhance the use of enabling technology, in particular information and communications technology, to promote the empowerment of women**
>
> 5.b.1 Proportion of individuals who own a mobile telephone, by sex

This target is interpreted to cover research about the use of enabling tecnology to promote empowerment of women. 

As both the target and the indicator emphasize ICT, we have an extra focus on ICT. However, all forms of enabling technologies may be included as relevant as long as they promote the empowerment of women.

United Nations' "Women’s Empowerment, SDGs and ICT", https://www.unapcict.org/sites/default/files/inline-files/Module_C1.pdf, defines ICT as: "ICT refers to all technology for creating, manipulating, storing, managing, sending and receiving information. ICT encompasses a wide range of multimedia and communication
tools. It can include, but is not limited to, old media such as radio, television and telephone,
as well as new media networks (fixed or wireless Internet), hardware (computers, mobile
phones, tablets, etc.) and software (social media services, multimedia applications, mobile apps, etc.)" (p. 31)

For definitions of gender equality and empowerment we use "Gender equality: Glossary of Terms and Concepts" from UNICEF: (https://www.unicef.org/rosa/media/1761/file/Genderglossarytermsandconcepts.pdf )

This query consists of 1? phrases......


## Phrase 1

The basic structure is _use_ + _technologies_ + _empowerment of women_

```py
TS=
(

)
```

### Target 5.c

> **5.c Adopt and strengthen sound policies and enforceable legislation for the promotion of gender equality and the empowerment of all women and girls at all levels**
>
> 5.c.1 Proportion of countries with systems to track and make public allocations for gender equality and women’s empowerment

This target is interpreted to cover research about policies and legislation for the promotion of gender equality and for the empowerment of women and girls. According to Indicator metadata 5.c (https://unstats.un.org/sdgs/metadata/files/Metadata-05-0c-01.pdf ) we interpret the indicator to pertain to the characteristics of the financial system, not to the amount of funds each country spends on efforts for gender equality.

For definitions of _gender equality_ and _empowerment_ we use "Gender equality: Glossary of Terms and Concepts" from UNICEF: (https://www.unicef.org/rosa/media/1761/file/Genderglossarytermsandconcepts.pdf )

This query consists of X phrases......


## Phrase 1

The basic structure is _policies/legislation_ + _gender equality/empowerment of women_  

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

<span id="f1li">UN. (1995).</span> *Report of the Fourth World
Conference on Women*. https://www.un.org/womenwatch/daw/beijing/pdf/Beijing%20full%20report%20E.pdf [Accessed 2025.06.05]


<span id="f2li">UN. (xxxx).</span> *title   ... *. https://www.un.....  [Accessed 2025.06.05]


<span id="f3li">UN Women. (2015).</span> *Monitoring Gender Equality and the Empowerment of women and girls in the 2030 Agenda for Sustainable Development: Opportunities and Challenges: Position Paper*. https://www.unwomen.org/sites/default/files/Headquarters/Attachments/Sections/Library/Publications/2015/IndicatorPaper-EN-FINAL.pdf    [Accessed 2025.06.05]


<span id="f4li">xxx. (xxxx).</span> *title... *. https://www.u... [Accessed 2025.06.05]