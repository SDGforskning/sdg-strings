# Search query for SDG 16 - Peace, justice and strong instutitions, Bergen topic-approach.

Promote peaceful and inclusive societies for sustainable development, provide access to justice for all and build effective, accountable and inclusive institutions at all levels 

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the topics in the SDG 16 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in the SDG 16 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

## 3. Targets

### Target 16.1

> **16.1 Significantly reduce all forms of violence and related death rates everywhere**
>
> 16.1.1 Number of victims of intentional homicide per 100,000 population, by sex and age
>
> 16.1.2 Conflict-related deaths per 100,000 population, by sex, age and cause
>
> 16.1.3 Proportion of population subjected to (a) physical violence, (b) psychological violence and/or (c) sexual violence in the previous 12 months
>
> 16.1.4 Proportion of population that feel safe walking alone around the area they live after dark
>

This target is interpreted to cover research about

 •	reduction of violence and intentional killings.

According to United Nations violence is defined as 
>“(...) a social phenomenon that involves forceful acts or behaviour that are intended to cause harm.
>The injury or damage inflicted by violence to an individual or  collective group may be physical, psychological,
>sexual, or deprivation, or combined. Violence is both intentional and forceful (Adapted from Jacquette, 2013).”
>: https://www.undrr.org/understanding-disaster-risk/terminology/hips/so0301 
 
Conflicts are often the cause of violence, hence the notions are closely linked to each other. Here the focus is on conflicts where the intention is violent harm, whether the conflicts are interpersonal (like family violence, neighbour’s disputes, robberies etc.), killings by criminal organizations, domestic political conflicts like civil wars, or international armed conflicts, such as wars.  (see https://unstats.un.org/sdgs/report/2025/The-Sustainable-Development-Goals-Report-2025.pdf)  Further, armed conflicts are defined as 
>"... all cases of declared war and other de facto armed conflict between two or more States, even if the state of war is not recognised by one of them and/or the use of armed force is unilateral (ICRC, 2024).”:
> https://www.undrr.org/understanding-disaster-risk/terminology/hips/so0101

The query should also find research on work for peace as an aspect of reducing violence.

The violence is of different character and is reported from all over the world, hence no definition or limitation to particular geographical areas or states in the query.

This query is dived in 4 phrases according to different aspects of violence. 

#### Phrase 1

The topic search on violence in general consist of expressions for violence or violent conduct/behaviour. The word "killing" is much in use in health, typically when fighting cancer or bacterias, but also in other contexts like hunting, animals, bugs etc., and is therefore restircted in the query accordingly: Killings + people/humans, Killings + mass/revenge

```py

TS=
(
    "Violence" OR "terrorism" OR "massacre" OR "genocide" OR "Pogrom$" OR "ethnic cleansing"
    OR "rape$" OR raping$ OR "sexual assault" OR "torture" OR "assassination$" OR "murder$" OR "homicide$"
    OR "Terrorist attack" OR "terrorist related death$" OR "violent extremism" OR "religious violence" OR "deadly attack$"
    OR
        ("Killing$"
        NEAR/5
            ("citizen$" OR "civilian$" OR "soldier$" OR "people" OR "person$" OR "child*" OR "Young" OR "Youth" OR "adolescent$" OR "teen*"
            OR "men" OR "man" OR "women" OR "woman" OR "adult$" OR "elderly" OR "demograph*" OR "humans" OR "humanity" OR "human"
            )
        )
    OR
        ("Killing$"
        NEAR/5
            ("mass" OR "terror" OR "combat$" OR "war$" OR "revenge" OR "feud$" OR "School$"
            )
        )
)
```
#### Phrase 2 

This query consist of violent + war/warfare/conflict/attacks/riots. "Violence" is covered in phrase 1.

```py
TS=
(
    (
        ("Violent*" OR "armed" OR "deadl*")
        NEAR/3
            ("conflict*" OR "dispute*" OR "hostilit*" OR "feud$" OR "vendetta" OR "battle" OR "fight*" OR "attack*"
            OR "aggression$" OR "aggressive*" OR "assault*" OR "confrontation$" OR "combat*" OR "riot$" OR "coup$"
            OR "rebellion$" OR "uprising$" OR "invasion$"
            )
    ) 
OR
    (
        ("Military" OR "militia*" OR "paramilitary")
        NEAR/0
            ("conflict*" OR "dispute*" OR "hostilit*" OR "feud$" OR "vendetta" OR "battle" OR fight* OR "attack*"
            OR "aggression$" OR "aggressive*" OR "assault*" OR "confrontation$" OR "combat*" OR "riot$" OR "coup$"
            OR "rebellion$" OR "uprising$" OR "invasion$")
            )  
OR
    (
        ("Violent*" OR "Armed" OR "military" OR "militia*" OR "paramilitary") NEAR/3 ("war$" OR "warfare$")
    )
OR
    (
        ("Violent*" OR "armed" OR "military" OR "militia*" OR "paramilitary") NEAR/1 ("force*" OR "intervention$")
    ) 
OR 
    (
        ("Violent*" OR "armed") NEAR/3 ("death$" OR "fatalit*" OR "injur*")
    )
OR 
    (
        ("Violent" OR "armed") NEAR/1 ("Robberies" OR "Robbery")
    ) 
OR 
    ("weapon$"
    NEAR/5
        ("conflict*" OR "Dispute*" OR "Hostilit*" OR "feud$" OR "vendetta" OR "aggression$" OR "aggressive" OR "assault*"
        OR "confrontation$" OR "Robberies" OR "Robbery" OR "riot$" OR "coup$" OR "rebellion$" OR "uprising$" OR "invasion$"
        OR "death$" OR "injur*" OR "force$")
    )
OR
    ("Political*"
    NEAR/5
        ("conflict*" OR "dispute*" OR "hostilit*" OR "feud$" OR "vendetta" OR "battle" OR fight* OR "attack*"
        OR "aggression$" OR "aggressive*" OR "assault*" OR "terrorism" OR "combat$" OR "riot$" OR "coup$"
        OR "rebellion$" OR "uprising$")
    )
)
```
#### Prase 3 

Family violence is only partly covered by the query on violence and murder in phrase 1. The query in this phrase is more directly on family and partner violence expresse in a query on family/gender/partner + violence/abuse/maltreatment. Related is also a query covering violence/abuse/maltreatment + physical/mental, though this also covers situations outside family violence.


```py
TS=
(
    (
        (
            ("gender-based" OR "gendered" OR "partner" OR "wife$" OR "husband$" OR "spouse" OR "child*" OR "kid*"
            OR "Family" OR "relative$" OR "domestic" OR marital OR "honor-related" OR "sexual*")
            NEAR/3
                ("harassment" OR "abuse" OR "assault" OR "misuse" OR "maltreat*" OR "killing$")
        OR "uxoricide$"
        )
    ) 
OR 
    (
        (
            ("Physical*" OR "mental*" OR "emotional*" OR "psychological*")
            NEAR/1
                ("harassment" OR "abuse" OR "assault" OR "misuse" OR "maltreat*")
        )
    )
)
```

#### Phrase 4
The research on work for peace is research on the opposite of violence, research on work for stability and avoiding conflicts and killings. The query consist of peacebuilding.

```py
TS=
("peacebuilding" OR "peacekeeping" OR "sustainable peace" OR "disarmament*" OR "demilitarization$" OR "demilitarisation$"
    OR
    (
        ("peace*" OR "stabilit*" OR "securit*" OR "pacification")
        NEAR/3
            ("conflict*" OR "postconflict*" OR "violence")
    )
)

```



### Target 16.2

> **16.2 End abuse, exploitation, trafficking and all forms of violence against and torture of children**
>
> 16.2.1 Proportion of children aged 1–17 years who experienced any physical punishment and/or psychological aggression by caregivers in the past month
>
> 16.2.2 Number of victims of human trafficking per 100,000 population, by sex, age and form of exploitation
>
> 16.2.3 Proportion of young women and men aged 18–29 years who experienced sexual violence by age 18

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 16.3

> **16.3 Promote the rule of law at the national and international levels and ensure equal access to justice for all**
>
> 16.3.1 Proportion of victims of (a) physical, (b) psychological and/or (c) sexual violence in the previous 12 months who reported their victimization to competent authorities or other officially recognized conflict resolution mechanisms
>
> 16.3.2 Unsentenced detainees as a proportion of overall prison population
>
> 16.3.3 Proportion of the population who have experienced a dispute in the past two years and who accessed a formal or informal dispute resolution mechanism, by type of mechanism

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 16.4

> **16.4 By 2030, significantly reduce illicit financial and arms flows, strengthen the recovery and return of stolen assets and combat all forms of organized crime**
>
> 16.4.1 Total value of inward and outward illicit financial flows (in current United States dollars)
>
> 16.4.2 Proportion of seized, found or surrendered arms whose illicit origin or context has been traced or established by a competent authority in line with international instruments

This target is interpreted to cover research about 

- reduction of illicit financial flows (IFFs) 
- reduction of illicit arms flows 
- strengthening recovery of stolen assets 
- fighting all organized crime  
 
For research on reduction of illicit financial and arms flows, it should also cover research on strengthening the capacity to track and control illegal financial and arms flows in and out of countries. This includes research on capital and arms controls, tax evasion, business transparency, money laundering etc.  Illicit arms flows, recovery and returning stolen assets, illicit financial flows and organized crime are all closly interconnected. 

Assets in this context are defined as financial assets like cash and bank accounts, real estate like land and property, and valuables like for instance fine art, gold, crypto currency, private jets etc. 
Fighting organized crime can to a large extent include research on corruption, a theme covered broader in SDG 16.5. Substantially reduce corruption and bribery.  It can also cover human trafficking, a topic covered by 16.2. Protect children from abuse, exploitation, trafficking and violence.

https://sdg16now.org/report/target16-4/ 

The query consists of 4 phrases.

#### Phrase 1
This phrase is on research on work on reducing illicit financial flows (IFF) and consist of reducing + illicit/illegal + money transfer. The query expressing research on work to improve the control with IFFs, contains strengthening + business transparency.

```py
TS=

(
(
	("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "decreas*" OR "minimi*"
	OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "fight*" OR "abate$" OR "abating" OR "diminish*" OR "curb*")
	NEAR/5
    	(
			(
        	("illicit*" OR "illegal*" OR "crim*" or "unlawful*" OR "corrupt*" OR "fraud*")
        	NEAR/5
            	("financ*" OR "money" OR "cash" OR "capital" OR "economic*" OR "currenc*" OR "transaction$" OR trade OR "commercial practic*" OR "commercial activit*")
    		)
			OR "Tax evasion*" OR "Duty evasion" OR "Trade misinvoic*" OR "Money laundering" OR "Tax haven$" OR " Financial haven$"
			OR
				(
					("illicit*" OR "illegal*" OR "crim*" OR "unlawful*" OR "corrupt*" OR "fraud*")
					NEAR
						(
							("financ*" OR "money" OR "cash" OR "capital" OR "economic*") NEAR/3 ("Transfer*")
						)
				)
			OR
				(
					("business" OR "econom*" OR "financial" OR "marked" OR "corporate") NEAR/1 ("manipulation$" OR "fraud$" OR "Secre*")
				)
		)
	)
				OR
(
					("increas*" OR "strengthen*" OR "improv*" OR "better" OR "more efficient*" OR "more effectiv*" OR "develop" OR "developing"
					OR "encourag*" OR "facilitat*" OR "ensure")
					NEAR/5

				
						(
							(
        					("business" OR "economic*" OR "financial" OR "marked" OR "corporate") NEAR/1 ("transparen*")
    						)
								OR " ownership regist*" OR "Global Financial Integrity")
	
)	
				
	

)
```

#### Phrase 2
This phrase is about limiting the flow of illicit armaments, and the query contains limit + illicit + weapons. A closer proximity operator is used for illicit + arms to avoid litterature on arms as body parts. The search has to contain illicit/illegal, to avoid the litterature on legal weaponry. As the second half of the phrase is about finding research on control with the flow of illigeal weapons, the\is part of the query consist of strengthening + tracing + weapons/weaponization.

```py
TS=
(
	("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*"
	OR "combat*" OR "decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited"
	OR "mitigat*" OR "fight*" OR "abate$" OR "abating" OR "diminish*" OR "curb*")
	NEAR/5
		(
    		("Illicit" OR "illegal*" OR "crim*" or "unlawful*" OR "diversion" OR "diverted" OR "privately manufactured")
    		NEAR/5
        	("armament$" OR "firearm$" OR "weapon*" OR "ammunition$" OR "munition$" OR "gun$" OR "handgun$"
			OR "artiller*") 
			OR
    			("arms"
				NEAR/0
					("Illicit" OR "illegal*" OR "crim*" or "unlawful*" OR "diversion" OR "diverted" OR "privately manufactured")
				)
			OR
    			(
        			("Trafficking" OR "smuggl*")
        			NEAR/1
            			("arms" OR "armament$" OR "firearm$" OR "weapon$" OR "weaponry" OR "ammunition$" OR "munition$"
						OR "gun$" OR "handgun$" OR "artiller*")
    			)
		)
	OR
		(
			("increas*" OR "strengthen*" OR "improv*" OR "better" OR "more efficient*" OR "more effectiv*"
			OR "develop" OR "developing" OR "encourag*" OR "facilitat*")
			NEAR/5
				(
					("Tracing" OR "Trace*" OR "Track$" OR "seizures" OR "Identif*" OR "record*" OR "control"
					OR "national registr*" OR "foreign registr*")
					NEAR/5
						("small arms" OR "armament$" OR "firearm$" OR "weapon*" OR "ammunition$" OR "munition$"
						OR "gun$" OR "handgun$" OR "artiller*")
				
				OR
        					(
            					(
                					("Tracing" OR "Trace*" OR "track$" OR "seizures" OR "Identif*" OR "record*" OR "control"
									OR "national registr*" OR "foreign registr*")
                					NEAR/0 ("arms")
            					)
        					)
				)

	OR
		("Small Arms Trade Transparency Barometer" OR "Arms Trade Treaty" OR "Register of Conventional Arms") 
					)

)
```

#### Phrase 3

```py
TS=
(

)
```

#### Phrase 4

```py
TS=
(

)
```

### Target 16.5

> **16.5 Substantially reduce corruption and bribery in all their forms**
>
> 16.5.1 Proportion of persons who had at least one contact with a public official and who paid a bribe to a public official, or were asked for a bribe by those public officials, during the previous 12 months
>
> 16.5.2 Proportion of businesses that had at least one contact with a public official and that paid a bribe to a public official, or were asked for a bribe by those public officials during the previous 12 months

This query consists of X phrases.

```py
TS=
(

)
```

### Target 16.6

> **16.6 Develop effective, accountable and transparent institutions at all levels**
>
> 16.6.1 Primary government expenditures as a proportion of original approved budget, by sector (or by budget codes or similar)
>
> 16.6.2 Proportion of population satisfied with their last experience of public services

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 16.7

> **16.7 Ensure responsive, inclusive, participatory and representative decision-making at all levels**
>
> 16.7.1 Proportions of positions in national and local institutions, including (a) the legislatures; (b) the public service; and (c) the judiciary, compared to national distributions, by sex, age, persons with disabilities and population groups
>
> 16.7.2 Proportion of population who believe decision-making is inclusive and responsive, by sex, age, disability and population group

This target is interpreted to cover research about 
-	ensuring responsive decision-making institutions
-	ensuring decision-making institutions are inclusive
-	ensuring participatory decision-making institutions 
-	ensuring representative decision-making institutions
across demographic groups or population groups, in local, national and international decision-making institutions. 

Decision-making institutions are here understood as legislature, public service and judiciary institutions.  Judicial institutions are understood as covering the courts of law at all levels. These institutions as well as legislatures and public services, are named at a generic level.  

Minority groups, including political minorities, or according to sex, sexual orientation, disability, age, ethnicity, religion, etc., that are underrepresented or unrepresented in decision-making institutions, are not explicitly named in the search string. The theory is that they will anyhow be retrieved by the query asking for responsive, inclusive, participatory and representative decision-making institutions. This also avoid the risk that a few unmentioned groups are not covered by the query.

The target is divided in 4 phrases:
-	Governance, on national and local level
-	The legislatures
-	The public service
-	The judiciary
  
#### Phrase 1

```py
TS=
(

)
```
#### Phrase 2

```py
TS=
(

)
```
#### Phrase 3

```py
TS=
(

)
```
#### Phrase 4

```py
TS=
(

)
```

### Target 16.8

> **16.8 Broaden and strengthen the participation of developing countries in the institutions of global governance**
>
> 16.8.1 Proportion of members and voting rights of developing countries in international organizations

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 16.9

> **16.9 By 2030, provide legal identity for all, including birth registration**
>
> 16.9.1 Proportion of children under 5 years of age whose births have been registered with a civil authority, by age

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 16.10

> **16.10 Ensure public access to information and protect fundamental freedoms, in accordance with national legislation and international agreements**
>
> 16.10.1 Number of verified cases of killing, kidnapping, enforced disappearance, arbitrary detention and torture of journalists, associated media personnel, trade unionists and human rights advocates in the previous 12 months
>
> 16.10.2 Number of countries that adopt and implement constitutional, statutory and/or policy guarantees for public access to information

This target is interpreted to cover research about 
- Ensuring public access to information.  
The other side of the coin as avoiding disinformation and fake news. For a description on the topic disinformation:
>“While misinformation refers to the accidental spread of inaccurate information, disinformation is not only inaccurate, but intends to deceive and is spread in order to do serious harm.
>Disinformation can be spread by state or non-state actors. It can affect a broad range of human rights, undermining responses to public policies or amplifying tensions in times of emergency or armed conflict.
>There is no universally accepted definition of disinformation. No one definition may be sufficient on its own, given the multiple and different contexts in which concerns over disinformation may arise, including with >regard to issues as diverse as electoral process, public health, armed conflicts, or climate change.” See https://www.un.org/en/countering-disinformation
- protection of fundamental freedoms. Fundamental freedoms are here interpreted as part of basic human rights, like 
    “ ...freedom of speech, freedom of worship, freedom from want and freedom from fear...” 
    (https://www.ohchr.org/en/human-rights/universal-declaration/translations/english)
- ensuring public access to information about the extent of killings, kidnapping, violence against and disappearance of typically journalists, media personnel, trade unionist and human rights advocates

All parts of the target should be in accordance with national laws and international agreements.  It also includes research about implementation and adaption of constitutional, statutory or policy guarantees for public access to information 

“The four freedoms relate to freedom of speech, freedom of worship, freedom from want and freedom from fear. They are sometimes simply referred to as freedom from fear and freedom from want.” https://www.ohchr.org/en/human-rights/universal-declaration/translations/english 

For definition of right to information, see Unesco’s information: https://www.unesco.org/en/right-information

It should include research about implementation and adaption of constitutional, statutory or policy guarantees for public access to information.
Unavoidably the find (hits) will contain all sorts of topics as it is about access to information on anything, like politics, environment, health, urban planning etc, no restriction according to topic.

The query consist of three phrases:
- Public access to information
- Killings and kidnapping of journalists
- Fundamental freedoms for everyone

#### Phrase 1

```py
TS=
(

)
```
#### Phrase 2

```py
TS=
(

)
```
#### Phrase 3

```py
TS=
(

)
```

### Target 16.a

> **16.a Strengthen relevant national institutions, including through international cooperation, for building capacity at all levels, in particular in developing countries, to prevent violence and combat terrorism and crime**
>
> 16.a.1 Existence of independent national human rights institutions in compliance with the Paris Principles

This target is interpreted to cover research about 

```py
TS=
(

)
```

### Target 16.b

> **16.b Promote and enforce non-discriminatory laws and policies for sustainable development**
>
> 16.b.1 Proportion of population reporting having personally felt discriminated against or harassed in the previous 12 months on the basis of a ground of discrimination prohibited under international human rights law

This target is interpreted to cover research about 

```py
TS=
(

)
```


## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f1">UN DESA. (2025).</span> *Goals: Promote peaceful and inclusive societies for sustainable development, provide access to justice for all and build effective, accountable and inclusive institutions at all levels*. https://sdgs.un.org/goals/goal16#targets_and_indicators [Accessed 2025.06.27]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/
