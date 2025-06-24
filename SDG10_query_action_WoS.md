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

Acronyms used:

    UN DESA: UN Department of Economic and Social Affairs
    IHRL: International Human Rights Law
    ODA: Official Development Assistance
    SDT: Special and Differential Treatment

## 3. Targets

### Target 10.1

> **10.1 By 2030, progressively achieve and sustain income growth of the bottom 40 per cent of the population at a rate higher than the national average**
>
> 10.1.1 Growth rates of household expenditure or income per capita among the bottom 40 per cent of the population and the total population

This target is interpreted as to cover research about how to raise and sustain the income growth rate of the poorest population.

Setting the limit to the bottom 40 % is a "practical compromise" that insures the target including the poorest populations in differing circumstances of different countries. The income growth rate is computed as average annual growth rate of either per capita consumption or actual income over about a 5-year period. (UN Statistics Divison 2024a.)  

This query consists of 1 phrase. The basic structure is *action + income growth + poor*

```py
TS=
((("bottom 40%" or "bottom 40 percent" or "bottom 40 per cent" or "the poor" or "poverty" or "the poorest" or "rural poor" or "urban poor" or "working poor" or "destitute$" or "low income" or "low-income" or "disadvantaged" or "unemployed") NEAR/3 ("household$" OR "people" OR "family" or "families"))

("income growth" or "income growth rate" or "per capita consumption" or "per capita income" or "welfare aggregate" or "shared prosperity" or "welfare distribution" OR "inclusive growth")

"rais*" or "foster*" or "increas*" or "promot*" or "boost*" or "enhanc* or "improv*" or "better" or "attain*" or "achiev*" or "provid*" or "ensur*" or "guarantee*" or "maintain*" or "secur*" or "strengthen*" or "develop*" or "establish*" or "sustain*" or "standardi*" or "regulari*" or "consolidat*" 

or "stabili*" or "normali*" or "uphold*" or "or "stabili*" or "normali*" or "uphold" or "stable" or "fixed" or "perpetual*" or "lasting" or "enduring"

)
```

### Target 10.2

> **10.2 By 2030, empower and promote the social, economic and political inclusion of all, irrespective of age, sex, disability, race, ethnicity, origin, religion or economic or other status**
>
> 10.2.1 Proportion of people living below 50 per cent of median income, by sex, age and persons with disabilities

This target is interpreted to cover research about enabling and promoting everyone to participate in social, economic and political activities. Special attention is paid to people in a disadvantaged position due to any characteristic, e.g. age, gender or disability (horizontal inequalities).

This target handles empowering people who face horizontal inequalities. This refers to groups of people who share an identity characteristic like race or religion and can therefore be exposed to the same kind of inequalities. (Stewart 2016). Ensuring that people in disadvantaged positions are part of decision-making processes (especially decisions regarding themselves) is a method recommended to accelerate progress in this target as well as the whole of SDG10 (United Nations 2024). A big part of structural discrimination and horizontal inequalities are linked to poorness, which is why living below 50 % of median income is considered a solid indicator for this target (Sharif 2024; World Bank Group 2025). For example, persons with disabilities and people of African descent experience significantly higher levels of poverty (United Nations 2018; World Bank Group 2025). 

Social inclusion means improving opportunities for individuals and groups to take part in society. This can include for example eradicating discriminatory attitudes from legal systems, labour markets and health care. (World Bank Group 2025.) Economic inclusion aims to empower individuals and communities by for example boosting their income and training them in economic skills (Sharif 2024). Political inclusion then covers opportunities for partaking in political activities, e.g. voting and participating in elections (Aldar ym. 2025).


```py
TS=
(("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "living in poverty"
    OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
    OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" 
    OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
    OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
    OR (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
    OR "disabled" OR "disabilities" OR "disability"
    OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
    OR "unemployed" 
    OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*" OR "accident$"))
    OR "women" OR "woman" OR "girls" OR "girl"
    OR "pregnant" OR "pregnancy" OR "maternity"
    OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
    OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
    OR "living with HIV" OR "living with AIDS"
    OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
    OR "indigenous group$"
    )

"increas*"
"strengthen*"
"improv*"
"restor*"
"enhanc*"
"better"
"more efficient"
"higher"
"upgrad*"
"scal* up"
"build*" ("build* capacity" / "capacity building" / "capacity development")
"expand" OR "expansion*"
"accelerat*"
"advance" OR "advancing"
"develop" OR "developing"
"empower*"
"promot*"
"ensure"
"attain*"
"achiev*" - note, see lower for own section on establishing/achieving

"social* inclusi*"
"economic* inclusi*"
"political* inclusi*"
"societal activit*"

"decreas*"
"minimi*"
"reduc*"
"restrict*"
"limit$"
"limiting"
"limited"
"mitigat*"
"degrad*"
"tackl*"
"alleviat*"
"lowering"
"lower$"
"lowered"
"fight*"
"combat*"
"declin*"
"stop*"
"end"
"ends"
"ended"
"ending"
"remov*"
"eliminat*"
"eradicat*"
"avoid*"
"prevent*"
"combat*"
"cure"
"halt*"
"resist*"
"overcome"

"horizontal inequalit*"
"social* exclusi*"
"economic* exclusi*"
"political* exclusi*"
)
```

### Target 10.3

> **10.3 Ensure equal opportunity and reduce inequalities of outcome, including by eliminating discriminatory laws, policies and practices and promoting appropriate legislation, policies and action in this regard**
>
> 10.3.1 Proportion of population reporting having personally felt discriminated against or harassed within the previous 12 months on the basis of a ground of discrimination prohibited under international human rights law

This target is interpreted to cover research about eliminating discriminatory legislation, policies and other practices and promote ones that ensure equal opportunity and reduce inequalities of outcome.

"Discrimination is any distinction, exclusion, restriction or preference or other differential treatment that is directly or indirectly based on prohibited grounds of discrimination, and which has the intention or effect of nullifying or impairing the recognition, enjoyment or exercise, on an equal footing, of human rights and fundamental freedoms in the political, economic, social, cultural or any other field of public life." The prohibited grounds of discrimination are listed in IHRL (UN Statistics Division 2024b.)

```py
TS=
(

)
```

### Target 10.4

> **10.4 Adopt policies, especially fiscal, wage and social protection policies, and progressively achieve greater equality**
>
> 10.4.1 Labour share of GDP
>
> 10.4.2 Redistributive impact of fiscal policy

This target is interpreted to cover research about promoting the implementation of existing or new social and economic policy practices to reduce inequalities/achieve greater equality.

```py
TS=
(

)
```

### Target 10.5

> **10.5 Improve the regulation and monitoring of global financial markets and institutions and strengthen the implementation of such regulations**
>
> 10.5.1 Financial Soundness Indicators

This target is interpreted to cover research about improving the regulation and monitoring of global financial markets and institutions.

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

This target is interpreted to cover research about enhancing the representation and decision-making powers of developing countries in international economic institutions.

In order to achieve truely effective and permanent changes on a global level, it is crucial to involve developing countries in the decision-making processes that concern their own economical development as well (UN DESA 2019; UN 2024).

```py
TS=
(

)
```

### Target 10.7

> **10.7 Facilitate orderly, safe, regular and responsible migration and mobility of people, including through the implementation of planned and well-managed migration policies**
>
> 10.7.1 Recruitment cost borne by employee as a proportion of monthly income earned in country of destination
>
> 10.7.2 Number of countries with migration policies that facilitate orderly, safe, regular and responsible migration and mobility of people
>
> 10.7.3 Number of people who died or disappeared in the process of migration towards an international destination
>
> 10.7.4 Proportion of the population who are refugees, by country of origin

This target is interpreted to cover research about ensuring safe, responsible and regular migration and mobility of people.

```py
TS=
(

)
```

### Target 10.a

> **10.a Implement the principle of special and differential treatment for developing countries, in particular least developed countries, in accordance with World Trade Organization agreements**
>
> 10.a.1 Proportion of tariff lines applied to imports from least developed countries and developing countries with zero-tariff

This target is interpreted to cover research about implementing the principle of special and differential treatment (SDT) for developing countries, in accordance with the World Trade Organisation agreements.

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
* ensuring official development assistance (ODA) and financial flows are targeted to where the need is greatest
* dividing the resources in accordance with the national, regional and local plans of the recipient countries.

We have two bullet-points here to put emphasis on targeting assets where they are needed most, as well as localization as per portrayed in Inter-Agency Policy Brief: Accelerating SDG Localization to deliver on the promise of the 2030 Agenda for Sustainable Development (UN 2024).

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
This target is interpreted to cover research about reducing the transaction cost of migrant remittances and eliminating corridors of high costs.

```py
TS=
(

)
```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

Aldar, L., Pliskin, R., Hasson, Y. & Halperin, E. (2025). Legitimizing inclusion: Psychological interventions increase support for minority inclusion in the political game, but less so during wartime. Political Psychology. https://doi.org/10.1111/pops.70030

Sharif, I. (2024). Why economic inclusion is key to reducing poverty and empowering people. World Bank Blogs. https://blogs.worldbank.org/en/voices/why-economic-inclusion-is-key-to-reducing-poverty-and-empowering-people

Stewart, F. (2016). Horizontal Inequalities. World Social Science Report 2016. ISSC. https://en.unesco.org/inclusivepolicylab/sites/default/files/analytics/document/2018/9/wssr_2016_chap_07.pdf

UN DESA. (11.7.2019). Review of SDG implementation and interrelations among goals: Discussion on SDG 10 – Reduced inequalities, Background Note. https://sdgs.un.org/sites/default/files/documents/24021BN_SDG_10_Inequalities.pdf

<span id="f1">UN DESA. (2025).</span> *Goals: Reduce inequality within and among countries*. https://sdgs.un.org/goals/goal10#targets_and_indicators [Accessed 2025.04.02]

UN Statistics Division (2024a). SDG Indicators Metadata Repository - Target 10.1. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-01-01.pdf

UN Statistics Division (2024b). SDG Indicators Metadata Repository - Target 10.3. Department of Economic and Social Affairs. https://unstats.un.org/sdgs/metadata/files/Metadata-10-03-01.pdf

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

United Nations (2018). High-level Political Forum 2018 - Inclusive, Safe, Resilient and Sustainable Societies and Persons with Disabilities. https://sustainabledevelopment.un.org/content/documents/18805PersonswithDisabilities_Sectoral_paper_HLPF2018.pdf

United Nations (2024). Inter-Agency Policy Brief: Accelerating SDG Localization to deliver on the promise of the 2030 Agenda for Sustainable Development. https://sdgs.un.org/publications/inter-agency-policy-brief-accelerating-sdg-localization-deliver-promise-2030-agenda.

World Bank Group (2025). Social inclusion. https://www.worldbank.org/en/topic/social-inclusion#1 [Accessed 17.06.2025]
