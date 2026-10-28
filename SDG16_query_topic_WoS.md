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
- the rule of law at the national and international levels
- equal access to justice for all

This includes:
- reporting of physical, psychological and sexual violence to competent authorities
- unsentenced prisoners and pretrial detention
- prison conditions, including health care, safety, food and space (overcrowding)
- rehabilitation and social reintegration of convicted/sentenced criminals
- formal or informal dispute resolution mechanisms as a way of solving disputes
- 
For the United Nations (UN) system, the rule of law is a principle of governance in which all persons, institutions and entities, public and private, including the State itself, are accountable to laws that are publicly promulgated, equally enforced and independently adjudicated, and which are consistent with international human rights norms and standards. It requires measures to ensure adherence to the principles of supremacy of the law, equality before the law, accountability to the law, fairness in the application of the law, separation of powers, participation in decision-making, legal certainty, avoidance of arbitrariness, and procedural and legal transparency. https://www.un.org/ruleoflaw/what-is-the-rule-of-law/
Justice for all is defined as fair, transparent, effective, non-discriminatory and accountable justice services for all people. https://www.un.org/ruleoflaw/thematic-areas/justice-2/

This query consists of 6 phrases.

#### Phrase 1
This phrase searches for the rule of law.

```py
TS=
(
	("law" OR "legal*")
	NEAR/1
	("rule" OR "supremacy" OR "equal*" OR "accountab*" OR "fair*" OR "certainty" OR "transparent" OR "transparency" OR "independen*" OR
  	("avoid*" NEAR/1 "arbitrar*") OR ("participat*" NEAR/1 "decision-making") OR "separation of power*"
	)
)
```
#### Phrase 2
This phrase searches for justice for all.In addition to the search for the term "justice for all", the phrase also searches for variations of a fair, non-discriminatory etc. justice system. 

```py
TS=
(
  	"justice for all" OR 
	(
		("Justice" OR "judicial system*" OR "legal system*")
		NEAR/2
		("fair*" OR "transparent" OR "effective" OR "non-discriminatory" OR "discriminat*" OR "accountable" OR "equal*" OR "access*")
	)
 )
```
#### Phrase 3
This phrase searches for pretrial detention, including variations of imprisonment without sentence.

```py
TS=
(
	("unsentence*" OR "without sentence" OR "without sentencing" OR "without conviction" OR "pretrial")
  	NEAR/1
  	("imprisonment" OR "prison" OR "detention" OR "incarcerat*" OR "custody" OR "remand*")
)
```
#### Phrase 4
This phrase searches for prison conditions and (or) prison overcrowding.

```py
TS=
(
	(
   		("imprisonment" OR "prison*" OR "detention" OR "incarcerat*" OR "inmate$" OR "remand*" OR "custody")
   		NEAR/1
   		("condition$" OR "food" OR "space" OR "health*" OR "medical")
  	)
	OR
 	(
  		("decreas*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "alleviat*")
  		NEAR/5
  		(
   			("imprisonment" OR "prison*" OR "detention" OR "incarcerat*" OR "inmate$" OR "custody" OR "remand*")
			NEAR/1 "overcrowd*"
		)
  	)
)
```
#### Phrase 5 
This phrase seraches for the rehabilitation of prisoners. 

```py
TS=
(
	("rehabilitat*" OR "reintegrat*")
	NEAR/1
	("imprisonment" OR "prison*" OR "criminal$" OR "inmate$" OR "incarcerat*")
)
```
#### Phrase 6 
This phrase searches for the reporting of violence and disputes to competent authorities and (or) the use of a formal or informal dispute resolution mechanism. 

```py
TS=
(
	(
		(
   			("dispute*" OR "conflict*" OR "argument*" OR "disagree*" OR "feud*" OR "violence")
  			NEAR/1
   			("solve" OR "solving" OR "resolve" OR "resolving" OR "work out" OR "interpret*" OR "resolution" OR "report")
		)
	NEAR/3
   		("Court*" OR "mechanism*" OR "process*" OR "method*" OR "committee*" OR "law*" OR "legal*" OR "justice" OR
		"judicial system*" OR "council$" OR "ombudsman" OR "tribunal$")
	)
	OR
  	(
   		("dispute*" OR "conflict*" OR "argument*" OR "disagree*" OR "feud*" OR "violence")
		NEAR/1 "mediat*"
	)
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
This phrase is about research on the increased work for recovery of stolen assets. Return, as a synonym of recovery, needs a seperate search query as its double meaning will give hits on the return on money. 
The structure of the query is recovery/return + stolen assets
https://www.u4.no/publications/the-recovery-of-stolen-assets-a-fundamental-principle-of-the-un-convention-against-corruption

```py
TS=
(
(
	(
		("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "more efficient*" OR "more effectiv*" OR "upgrad*" OR "scal* up"
		OR "build* capacity" OR "capacity building" OR "capacity development" OR "develop" OR "developing" OR "encourag*" OR "facilitat*")
		NEAR/5
			(
				(("return*" ) NEAR/3 ("stolen" OR "Plunder*" OR "hidden" OR "secreted" OR "illicit*" OR "illegal*"))
				OR
					(
					("recover*" OR "recaptur*" OR "repossess*" OR "trac*" OR "identif*" OR "freez*" OR "seiz*" OR "confiscat*") 
					NEAR 
						(("stolen" OR "Plunder*" OR "hidden" OR "secreted" OR "illicit*" OR "illegal*")
						NEAR
							("asset$" OR "monies" OR "money" OR "cash" OR "funds" OR "finance*" OR "bank account$" OR "propert*" OR "real estate$"
							OR "valuables" OR "collectables" OR "fine art$" OR "gold*" OR "jewel*" OR "diamond$" OR "crypto" OR "bit coin$"
							OR "yacht$" OR "private jet$" OR "expensive car$" OR "share$" OR "stock" OR "security" OR "Ship$" OR "Vessel$" OR "cargo*"))
					)
				OR
					("anti-money laundering" OR "Stolen Asset Recovery Initiative")
				OR
					(
						("law" OR "act*" OR "regulat*" OR "rule" OR "rules" OR "legislat*" OR "judiciary" OR "agreement$" OR "treaty" OR "treaties"
						OR "strateg*" OR "framework$" OR "instrument$" OR "governance" OR "procedur*" OR "practice$" OR "action$" OR "principle$" OR "initiative*")
						NEAR
							(("stolen" OR "hidden" OR "secreted" OR "illicit*" OR "illegal*")
							NEAR/5
								("asset$" OR "monies" OR "money" OR "cash" OR "funds" OR "finance*" OR "bank account$" OR "property" OR "real estate" OR "valuables" OR "collectables" OR "fine art"
								OR "gold" OR "jewel*" OR "crypto" OR "bit coin" OR "yacht$" OR "private jet$" OR "expensive car$" OR "watches" OR  "shares" OR "stock" OR "security"
								OR "Ship$" OR "Vessel$" OR "cargo*"))
					)
			)
	)
)

)
```

#### Phrase 4
This phrase is about research on reducing organized crime. Parts of the subject will be covered by the queries in phrases 1-3 as the topics are interwoven with organized crime. The query is containg weakening/reducing/controlling + criminal organisations. Criminal organizations are often behind cyber crime, hence the phrase includes a query covering research on this aspect as well. 
https://www.unodc.org/unodc/en/organized-crime/intro.html

```py
TS=
(
("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "curb*" OR "decreas*"
	OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "mitigat*" OR "fight*" OR "abate$" OR "abating" OR "diminish*")
	NEAR/5
		("illicit*" OR "illegal*" OR "crim*" or "unlawful*" OR "corrupt*" OR "fraud*")
		NEAR/1
			("Organi*" OR "underworld$" OR "syndicate$" OR "enterprise$" OR "cartel$" OR "network$" OR "group$" OR "triad$"
			OR "Business" OR "firm$" OR "compan*" OR "professional*")
		OR
		("mafia$" OR "mafioso" OR "gangster$" OR "gang$" OR "Transnational crime" OR "International crime"
		OR "global crime" OR "Global Organized Crime Index" OR "Global Financial Integrity" OR "Trade-Based Money Laundering")
		OR
		(("ICT" OR "cyber*" OR "internet" OR "computer*" OR "crypto*" OR "block-chain" OR "New technologies")
		NEAR/3
			("illicit*" OR "illegal*" OR "crim*" or "unlawful*" OR "corrupt*" OR "fraud *" OR "deception*"))

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
- effective, accountable and transparent institutions at all levels.

Even if both public and private institutions could be included, the goal is interpreted to be about public institutions, since the two indicators point to this sector in measuring government expenditures and public services.
"Levels" include the local, national and international levels of institutions such as parliaments, ministries, local governments, law enforcers (police), courts, ombudsman institutions, UN, EU etc. 
The search includes both names of existing institutions and more generic terms.   

This query consists of one phrase that searches for effective, accountable or transparent institutions as well as the oposite, e.g. ineffective, unaccaoutable and non-transparent institutions. 

```py
TS=
(
	("Effective" OR "successful*" OR "effectual" OR "functional" OR "Accountab*" OR "Responsible" OR "Liable" OR "liability" OR "Answerable" OR
	"chargeable" OR "Reliab*" OR "Transparent" OR "transparency" OR "openness" OR "open" OR "corrupt*" OR "non-transparent" OR "ineffective" OR
	"unsuccessful*" OR "dysfunctional*" OR "Unaccountab*" OR "unresponsible" OR "Unreliab*" OR "discredit*" OR "bribe*"
	)
	NEAR/3
	(
		(
			("global" OR "international" OR "regional" OR "transnational" OR "multilateral" OR "worldwide" OR "world wide" OR "intergovernmental" OR "public"
			)
			NEAR/0
			("organization$" OR "organisation$" OR "institution$" OR "assembly" OR "forum" OR "union*" OR "alliance*" OR "agency" OR "council"
			)
		)
	OR "governing body" OR "government*" OR "Budget" OR "public service$" OR "Parliament*" OR "Ministries" OR "ministry" OR "Law enforce*" OR "Police" OR
	"Court of Law" OR "court of justice" OR "Ombudsman" OR "tribunal*" OR "UN" OR "United Nations" OR "International Criminal Court" OR
	"European court of human rights" OR "ECHR" OR "WTO" OR "World Trade Organization" OR "UNCTAD" OR "EU" OR "European Union" OR "MERCOSUR" OR
	"Mercado Común del Sur" OR "ASEAN" OR "Association of Southeast Asian Nations" OR "South Asian Association for Regional Cooperation" OR "SAARC" OR "NATO" OR
	"North Atlantic Treaty Organization" OR "Shanghai Cooperation Organisation" OR "OSCE" OR "Organization for Security and Co-operation in Europe" OR
	"African Union" OR "Economic Community of West African States" OR "OECD" OR "Organisation for Economic Co-operation and Development" OR "World Bank" OR
	"International Monetary Fund" OR "Asian Infrastructure Investment Bank" OR "Development Bank of Latin America" OR "ECB" OR "European Central Bank" OR
	"African development bank" OR "Asian development bank" OR "Organization of American States" OR "League of Arab States" OR "Arab League" OR "ITU" OR
	"UNESCO" OR "UNIDO" OR "Universal Postal Union" OR "UPU" OR "World Health Organization" OR "World Intellectual Property Organization" OR "WIPO" OR
	"World Meteorological Organization" OR "WMO" OR "WBG" OR "International Atomic Energy Agency" OR "IAEA" OR "International Organization for Migration" OR
	"IOM" OR "International Seabed Authority" OR "ISA" OR "International Tribunal for the Law of the Sea" OR "ITLOS" OR
	"Organisation for the Prohibition of Chemical Weapons" OR "OPCW" OR "Preparatory Commission for the Comprehensive Nuclear-Test-Ban Treaty Organization" OR
	"CTBTO" OR "ICC" OR "International Trade Centre" OR "ITC" OR "UNDP" OR "UNEP" OR "UNFPA" OR "UNCDF" OR "UNV" OR "UN-Habitat" OR "UNHABITAT" OR "UNICEF" OR
	"World Food Programme" OR "WFP" OR "UNHCR" OR "UNOPS" OR "UNRWA" OR "UN Women" OR "UNWOMEN" OR "Office for the Coordination of Humanitarian Affairs" OR
	"OCHA" OR "UNAIDS" OR "UNU" OR "UNITAR" OR "UNIDIR" OR "UNSSC" OR "Food and Agriculture Organization" OR "FAO" OR "International Civil Aviation Organization" OR
	"ICAO" OR "International Fund for Agricultural Development" OR "IFAD" OR "International Maritime Organization" OR "IMO" OR "International Telecommunication Union"
	)
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
This query consist of search for research on (accommodate/develope +) inclusive/accessible + governance/government

```py
TS=
(
(("Inclusiv*" OR "Accessibl*" OR "Diversit*" OR "Responsiv*" OR "Receptiv*" OR "Participat*" OR "partake*" OR "Take part" OR "Representative") NEAR/3 ("Governance" OR "Government" OR "Cabinet" OR "administration" OR "political power" OR "authority" OR "directorate" OR "ministry" OR "department" OR "governing bod*"))
OR
(("Exclusi*" OR "exclude*" OR inaccessible OR "Unresponsive" ) NEAR/3 ("Governance" OR "Government" OR "Cabinet" OR "administration" OR "political power" OR "authority"))
)
```
#### Phrase 2
This query consist of research on inclusive/accessible + the legislatures. Parts of the debate on the topic is about avoiding that majority groups exclude minorities, but as exclusive rights some times are used to benefit in particular earlier discriminated groups of people, this is not part of the search.

```py
TS=
(
	(("Inclusive" OR "Accessible" OR "Diversit*" OR "Responsive" OR "Unresponsive" OR "Receptive" OR "Participat*" OR "partake*" OR "Take part" OR "Representative")
	NEAR/5
		("Legislature" OR ("Legislative" NEAR/3 ("bod*" OR "assembl*" OR "Council$")) OR "Legislation$" OR "Congress" OR "Parliament$" OR "National Assembl*"
		OR "Senate" OR "House of Representatives" OR "House of Commons")) 
)
```
#### Phrase 3
This phrase consist of query concerning research on inclusive/accessible + public service


```py
TS=
(
	("Inclusive" OR "Accessible" OR "Diverse" OR "Responsive" OR "Unresponsive" OR "Receptive" OR "Exclusive" OR "excluding" OR "Participat*" OR "partaking" OR "Take part" OR "Representative")
	NEAR/5
		("public service$" OR "civil service$" OR "government service$" OR "Municipal service$" OR "Municipal Council$" OR "City Council$" OR "public sector$" OR "public utilit*")
)
```
#### Phrase 4
This query aim to find research on inclusive judiciary, and consist of inclusive/accessible + judiciary

```py
TS=
(
	("Inclusive" OR "Accessible" OR "Diverse" OR "Responsive" OR "Unresponsive" OR "Receptive" OR "Exclusive" OR "excluding"
	OR "Participat*" OR "partaking" OR "Take part" OR "Representative")
	NEAR/5
		("judiciar*" OR "courts" OR "court" OR "tribunal*")

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

This target is interpreted to cover research about legal identity and birth registration. A legal identity includes name, sex, place and date of birth and nationality.

The term "passport" is not included in the search as the results mostly include research about different kinds of passports 
and the document itself, such as biometrics, not about having an identity. The term "National ID" describes mostly ID-systems and is also not included.

This query consists of one phrase searching for legal identity or birth registration

(
	("Identity"
	NEAR/0
	("legal" OR "paper$" OR "certificate$" OR "credential$" OR "card$")
	)
	OR
	("birth"
	NEAR/1
	("certificate$" OR "credential$" OR "registrat*" OR "register$")
	)
 	OR "recognized as a person before the law"
) 

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
The query contains of search for ensuring public + access/ rights + information/news. It also contains the opposite of reducing/controlling + public + disinformation. The search is not searching public*, but public or publicly, to avoid literature on for instance publicity or publications.

```py
TS=
(
(
("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better" OR "more efficient*" OR "more effectiv*" OR "higher" OR "upgrad*" OR "scal* up" OR "build*" OR "expand" OR "expansion*" OR "accelerat*" OR "advance" OR "advancing" OR "develop" OR "developing" OR "encourag*" OR "facilitat*" OR "promot*" OR "raise" OR "raising" OR "raised" OR "foster*" OR "boost*" OR "ensure" OR "attain*" OR "achiev*" OR "maintain*" OR "preserv*" OR "establish*" OR "implement*" OR "plan" OR "plans" OR "planned" OR "planning" OR "adopt*" OR "introduc*" OR "develop" OR "development" OR "provid*" OR "sustain$" OR "sustaining" OR "ensure" OR "attain*" OR "achiev*")
NEAR/5
(
(
(("Public" OR "Publicly") NEAR/5 (("access*" OR "availab*") NEAR/5 ("information*" OR "news")))
OR
(("access" OR "rights" OR "right" OR "freedom$" OR "transparan*") NEAR/1 ("news" OR "documents"))
OR
(("ATI" OR "Access-to-information" OR "freedom of information") NEAR/5 ("law*" OR "framework$" OR "legislation$")) 
)
)
)
OR
(
("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "eliminat*" OR "eradicat*" OR "avoid*" OR "prevent*" OR "combat*" OR "decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "limit$" OR "limiting" OR "limited" OR "tackl*" OR "alleviat*" OR "lowering" OR "lower$" OR "lowered" OR "fight*" OR "combat*" OR "declin*" OR "abate$" OR "abating" OR "diminish*")
NEAR/5
("disinfor*" OR "misinform*" OR (("fake" OR "misleadning*") NEAR/3 ("information$" OR "news")) OR "deepfake$" OR "incorrect information" OR "false information" OR "inaccurate information")
)

)
```
#### Phrase 2
This phrase is concerning the fact that killings and kidnappings of journalist and media personell are a threat to access to information in a society. The query consist of killings/kidnapping/imprisonment + journalists/media staff

```py
TS=
(
	(("Killing$" OR "disappear$" OR "torture" OR "kidnapping" OR "detention" OR "imprison*" OR "custody" OR "incarceration")
	NEAR/3
		("journalis*" OR "media personnel" OR "media staff" OR "trade unionist$" OR "trades unionist$" OR "union member$" OR "trade unionism"
		OR "human rights advocate$" OR "rights defender$" OR "activist$"))
)
```
#### Phrase 3
This phrase is about protecting fundamental freedoms for everyone in a society, and the query is built on strengthening/protect + freedom/rights + information/assembly/belief

```py
TS=
(
	(
		(("Freedom$" OR "right$")
		NEAR/3
			("Information" OR "thought" OR "press" OR "opinion" OR "speech" OR "assembl*" OR "association*" OR "worship" OR "religious" OR "belief" OR "religion" OR "conscience"))
			OR
				"free press" OR "freedom from want" OR "freedom from fear"
	)
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
•	non-discriminatory laws and non-discriminatory policies in all areas and in all aspects of sustainable development 

"Sustainable development" is not a part of the search as it is considered implicit that all goals are about obtaining sustainable development. Further, this target is a so called "Means of implementation" target and is therefore foundational to realization of all targets under SDG16. 
Definition of discrimination from https://unstats.un.org/sdgs/metadata/files/Metadata-16-0b-01.pdf. "Discrimination is any distinction, exclusion, restriction or preference or other differential treatment that is directly or indirectly based on prohibited grounds of discrimination, and which has the intention or effect of nullifying or impairing the recognition, enjoyment or exercise, on an equal footing, of human rights and fundamental freedoms in the political, economic, social, cultural or any other field of public life."

This query consists of one phrase with the basic structure non-discriminatory OR discriminatory + laws OR policies.

```py
TS=
(
	(
		("equal" OR "equally" OR "equalit*" OR "anti discriminat*" OR "antidiscriminat*" OR "non-discriminat*" OR "inclusi*" OR "egalitar*" OR
		"equity" OR "fairness" OR "discriminat*" OR "inequalit*" OR "harass*" OR "racis*" OR "sexis*" OR "xenophob*" OR "homophob*" OR "transphob*" OR "stigma*" OR
		"ableis*" OR  "unequal*" OR "exclusion" OR "exclude$" OR "bias" OR "bias$ed" OR "obstacle$" OR "barrier$"
		)
		NEAR/3
		("law$" OR "policy" OR "policies" OR "legal*" OR "legislat*" OR "judicial" OR "judiciary" OR "agreement$" OR "treaty" OR "treaties" OR
		"strateg*" OR "governance" OR "rule" OR "rules" OR "procedur*" OR "principle$")
	)

)
```

## 4. Contributions

* v2.1.0: 

Specialist input: 

## 5. Footnotes

<span id="f1">UN DESA. (2025).</span> *Goals: Promote peaceful and inclusive societies for sustainable development, provide access to justice for all and build effective, accountable and inclusive institutions at all levels*. https://sdgs.un.org/goals/goal16#targets_and_indicators [Accessed 2025.06.27]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/
