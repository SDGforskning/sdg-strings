# Search query for SDG 9 - Industry, innovation and infrastructure, Bergen topic-approach.

Build resilient infrastructure, promote inclusive and sustainable industrialization and foster innovation 

**Status: This query is currently under development (2025)**

**Contents**

1. Full query
2. General notes
3. Documentation and string sections for each target
4. Contributions
5. Footnotes


## 1. Full query

## 2. General notes

This document contains search strings for finding publications related to the topics in the SDG 9 targets and indicators ("topic approach"; focus on recall, larger result set). We also have a version which finds publications related to the actions in the SDG 9 targets and indicators ("action approach"; focus on precision, smaller result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

Targets and Indicators were found from the UN Department of Economic and Social Affairs website <a href="#f1">(UN DESA, 2025)</a>.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) <a href="#f2">(United Nations, 2016, 2017, 2018, 2019, 2020, 2021)</a>. Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).


## 3. Targets

### Target 9.1

> **9.1 Develop quality, reliable, sustainable and resilient infrastructure, including regional and transborder infrastructure, to support economic development and human well-being, with a focus on affordable and equitable access for all**
>
> 9.1.1 Proportion of the rural population who live within 2 km of an all-season road
>
> 9.1.2 Passenger and freight volumes, by mode of transport

This target is interpreted to cover research about reliable, sustainable and resilient infrastructure that is affordable and equitable for all.  

We interpret infrastructure in this target as a broad and integrated system, consisting of both physical and institutional components. It includes so-called hard infrastructure, such as energy, transport, water, waste management and digital communication systems, as well as soft infrastructure, including human resources, institutional structures and policy frameworks <a href="#f4">(Soriano, A., Gaikwad. S., Stratton-Short. S., Bajpai, A, & Imbuye. J., 2022, 10 </a>; <a href="#f8">United Nations Environment Programme, 2021, 8)</a>.

Since infrastructure is understood broadly to encompass both so-called hard infrastructure and soft infrastructure, it is practically very difficult, if not impossible, to employ all the terms that can be used to describe it. We use commonly employed infrastructure-related terms, drawn from the following sources; <a href="#f4">Soriano et al., 2022</a>; <a href="#f8">United Nations Environment Programme, 2021</a>. Since the target indicators emphasize transport infrastructure, we have included terms related to transportation more broadly in the search.

We interpret economic and social well-being as an outcome of infrastructure development rather than the primary target itself, and therefore do not include related terms in the search phrase.

This query consists of one phrase.

#### Phrase 1

This phrase is about sustainable infrastructure that is affordable for all. Basic structure is *sustainable + infrastructure + affordable*.

```py
TS=
(
	("reliabl*" OR "sustainab*" OR "resilien*" OR "invulnerab*" OR "adaptab*" OR "flexib*" OR "recoverab*" OR "maintainable*" OR "renewabl*" OR "resource-efficien*" 
	OR "repairab*" OR "recyclab*" OR "reusab*" OR "ecofriendly" OR "eco-friendly" OR "environmentally friendly" OR "environmentally sound" OR "ecologically friendly" 
	OR "ecologically sound" OR "low* carbon" OR "green" OR "eco" OR "ecological" OR "nonpolluting" OR "non-polluting" OR "energy-efficient"
	) 
	NEAR/5 
        ("infrastruct*" 
		OR 	(("energy" OR "power" OR "electric*") 
			NEAR/1 ("infrastruct*" OR "supply" OR "supplies" OR "supplying" OR "solution$" OR "source*" OR "transmission" OR "transfer*" OR "distrib*" OR "connections" OR "structure*" OR "foundation")
			)  
        OR "energy system$" OR "power system$" OR "electrification" OR "lighting" 
        OR (("waste" OR "wastewater$" OR "sewage") NEAR/1 ("treatment" OR "collection" OR "management")) 
		OR "recycling system$" 
        OR "water supply" OR "drinking water" OR "potable water" OR "clean water" OR "sanitation" OR "drainage system$" OR "water and sanitation system$" OR "food supply"
        OR "telecommunication$" OR "digital communication$" OR "communication$" OR "digital solutions" OR "internet" OR "mobile network$"
        OR "public amenities" OR "rule of law" OR "juridical system$" OR "legal service$" OR "financial service$" OR "banking service$" 
		OR "education" OR "school$"
        OR "health care" OR "healthcare" OR "public service$"
        OR "buildings" OR "housing" OR "public spaces" 
		OR (("facility" OR "facilities") NEAR/1 ("service$" OR "medical" OR "sport*" OR "social" OR "public"))
		OR "disaster management" OR "disaster prevent*" OR ("disaster*" NEAR/3 "prepare*") OR "public alert*" OR "public warn*" OR "early warn*" 
		OR ("system$" NEAR/1 ("alert*" OR "warn*"))
        OR "air connection*" OR "airport*" OR "border crossing" OR "freight*" OR "harbor*" OR "harbour*" OR "ports" OR "maritime" OR "mass transit*" OR "mobility system$" 
        OR "public transport*" OR "public transit*" OR "rail" OR "rails" OR "railway*" OR "road" OR "roads"  OR "highway*" OR "rural access" OR "sea connection*" OR "sea route*" 
        OR "ship* route*" OR "transport" OR "transportation" OR "tunnel$" OR "urban mobility" OR "waterways" 
        )
	NEAR/5 
		("afford*" OR "equitab*" OR "equality" OR "equity" OR "low cost" OR "inexpensive" OR "reasonable" OR "moderate" OR "fair" OR "accessib*" OR "economical*" OR "cost-effective*" OR "cheap")
)
```

### Target 9.2

> **9.2 Promote inclusive and sustainable industrialization and, by 2030, significantly raise industry’s share of employment and gross domestic product, in line with national circumstances, and double its share in least developed countries**
>
> 9.2.1 Manufacturing value added as a proportion of GDP and per capita
>
> 9.2.2 Manufacturing employment as a proportion of total employment

This target is interpreted to cover research about inclusive and sustainable industrialization and the share of industry in both economic growth and employment.

The term industry is inherently ambiguous. In general usage, it refers to a specific sector of economic activity, such as agriculture, manufacturing or services. In economics, however, the term is understood more narrowly, typically referring to manufacturing activities. Also, the indicators for this target focus on the manufacturing sector <a href="#f1">(UN DESA 2025)</a>. We interpret the concept of industry more broadly than manufacturing, as the target itself uses both the terms industrialization and industry, which we interpret as referring to the broader phenomenon of industrial development, even though manufacturing often has the key role in it. This broader viewpoint is seen in many documents by United Nations organizations, such as the Lima Declaration: Towards Inclusive and Sustainable Industrial Development <a href="#f9">(United Nations Industrial Development Organization 2013)</a>.

We also interpret that the underlying idea behind the target is inclusive and sustainable industrial development (ISID). ISID is a concept developed by UNIDO and is defined to mean "Long-term industrialization that drives development along three aspects: creating shared prosperity by offering equal opportunities and equitable distribution of benefits to all; advancing economic competitiveness; and safeguarding the environment by decoupling the prosperity generated by industrial activities from excessive natural resource use and negative environmental impacts" <a href="#10">(United Nations Industrial Development Organization 2021, xvii)</a>.

This query consists of two phrases.

#### Phrase 1

This phrase is about sustainable infrastructure that is affordable for all. Basic structure is *inclusive/sustainable + industrialization*.

```py
TS=
(
    (
		("inclusiv*" OR "participatory" 
		OR (("worker*" OR "employee*") NEAR/1 ("participation" OR "equity" OR "reasonableness" OR "fairness" OR "justice")) 
		OR "equal opportunit*" OR "equitab*" OR "equality" OR "inclusion" OR "social responsibility" 
		OR "sustainab*" OR "renewabl*" OR "resource-efficien*" OR "repairab*" OR "recyclab*" OR "ecofriendly" OR "eco-friendly" OR "environmentally friendly" OR "environmentally sound" 
		OR "ecologically friendly" OR "ecologically sound" OR "low* carbon" OR "green" OR "eco" OR "ecological" OR "nonpollut*" OR "non-pollut*" OR "energy-efficien*" OR "energy-saving"
		) 
		NEAR/5 
			("industrialisat*" OR "industrializat*" 
			OR (("industrial" OR "industry" OR "industries") NEAR/1 ("sector$" OR "development" OR "transformation" OR "expansion"))
			)
	)
    OR 
	("ecoindustrial development" OR "eco-industrial development" OR "industry 5.0" OR "fifth industrial revolution")
)
```
#### Phrase 2
This phrase is about the share of industry in economic growth and employment. Basic structure is *industry + economic growth/employment*.

```py
TS=
(
	(
		("industrial sector$" OR "industry" OR "industries" OR "manufacturing")
		NEAR/3 
			("employment" OR "job$" 
			OR (("share" OR "proportion" OR "percentage") NEAR/1 ("workers" OR "workplace*" OR "work place*")) 
			OR "labor force" OR "labour force" 
			OR "gross domestic product" OR "GDP" 
			OR (("economic*" OR "economy") NEAR/2 ("growth" OR "output$" OR "performance*"))
			)
	) 
	OR (("industrial sector$" OR "industry" OR "industries" OR "manufacturing") NEAR/5 ("unemployment"))
)

```

### Target 9.3

> **9.3 Increase the access of small-scale industrial and other enterprises, in particular in developing countries, to financial services, including affordable credit, and their integration into value chains and markets**
>
> 9.3.1 Proportion of small-scale industries in total industry value added, based on (a) international classification and (b) national classifications
>
> 9.3.2 Proportion of small-scale industries with a loan or line of credit

This target is interpreted to cover research about: 
* Access to financial services for small-scale industrial and other enterprises, including affordable credit.
* Integration of small-scale industrial and other enterprises into value chains and their participation in both local and international markets.

According to Indicator metadata 9.3.1, we interpret the term "small-scale enterprises" as encompassing all small businesses, including those classified in smaller categories such as microenterprises <a href="#f3">(UN Statistics Division, 2025)</a>. 

According to the definition provided by <a href="#f7">the United Nations Department of Economic and Social Affairs (2023, p. 2)</a>, we understand that a value chain refers to the set of activities undertaken by companies and workers to move a product from its initial concept to end use and beyond. These activities encompass the entire production process, starting from development and continuing through to customer support. They may occur within a single enterprise or be distributed among multiple firms within a local economy or across different countries.

International trade grew significantly after 1990, and one major driver of this growth was the emergence of global value chains (GVCs). These chains are considered a key mechanism for creating jobs and fostering sustainable, inclusive economic growth. A global value chain is defined as: "…the series of stages in the production of a product or service for sale to consumers. Each stage adds value, and at least two stages are in different countries". <a href="#f5">(World Bank, 2020)</a>.

For these reasons, we include a broad range of search terms related to value chains and supply chains.

This query consists of two phrases.

#### Phrase 1

This phrase is about access of small-scale enterprises to financial services. Basic structure is *financial services + small-scale enterprises*.

```py
TS=
(
	("long-term finance*" OR "loan$" OR "lend* fund$" OR "lending" OR "credit$" OR "debt$" OR "financial instrument*" OR "microfinanc*" OR "micro-financ*" 
    OR "microinsurance" OR "micro-insurance" OR "microcredit" OR "micro-credit" OR "microloan$" OR "micro-loan$" 
	OR "banks" OR "a bank" OR "banking" OR "bank account$" OR "bank financ*" OR "community bank$" OR "access to bank*"
    OR "digital finance" OR "digital money" OR "mobile money" OR "digital currency" OR "electronic payments" OR "digital payment$" 
	OR "fintech" OR "mobile phone-based payment" OR "mobile payment" OR "mobile wallet" OR "entrepreneurial finance" 
    OR "savings" OR "insurance" 
	OR (("deposit*" OR "withdraw*" OR "transfer" OR "save" OR "borrow") NEAR/1 ("currency" OR "money"))
    OR "payment service$" OR "transfer service$" OR "transfer funds" OR "financial inclusion" OR "M-PESA"
    OR (("financial" OR "monetary") NEAR/1 ("asset*" OR "opportunit*" OR "resource*" OR "service*")) 
    OR (("advice" OR "training") NEAR/2 ("business" OR "company" OR "companies"))
	)
    NEAR/5
        (
			(("small" OR "small-scale" OR "micro" OR "micro-scale") NEAR/3 ("enterprise*" OR "business*" OR "industry" OR "industri*" OR "firm$" OR "company" OR "companies" OR "venture*"))
        	OR "microenterprise$" OR "microbusiness*" OR "micro and small enterprise$" OR "MSEs" OR "micro- and small-scale enterprise$" OR "small and micro business*" OR "SME" OR "SMEs"
        )
)
```
#### Phrase 2

This phrase is about integration of small-scale enterprises to value chains/market entry. Basic structure is *small-scale enterprises + value chains/market entry*.

```py
TS=
(
	(
		(("small" OR "small-scale" OR "micro" OR "micro-scale") NEAR/1 ("enterprise*" OR "business*" OR "industry" OR "industri*" OR "firm$" OR "company" OR "companies" OR "venture*")) 
		OR "microenterprise$" OR "microbusiness*" OR "micro and small enterprise$" OR "MSEs" OR "micro- and small-scale enterprise$" OR "small and micro business*" OR "SME" OR "SMEs"
	)
	NEAR/5
		("value chain$" OR "production chain$" OR "supply chain$" OR "distribution chain$" OR "logistics chain$" OR "marketing chain$" OR "GVC*" OR "production network$" OR "processing chain$" 
		OR "retail chain$" OR "delivery chain$" OR "global commodity chain$" OR "supply network*" OR "material chain$" OR "global factory" OR "export*" OR "import" OR "market" OR "markets"  
		OR "cross-border business*" OR "internationali$ation" 
		OR (("international*" OR "local" OR "global" OR "globally" OR "regional*" OR "provincial*" OR "domestic") NEAR/3 ("networks" OR "business*" OR "trade" OR "factory" OR "factories"))
		)
)
```

### Target 9.4

> **9.4 By 2030, upgrade infrastructure and retrofit industries to make them sustainable, with increased resource-use efficiency and greater adoption of clean and environmentally sound technologies and industrial processes, with all countries taking action in accordance with their respective capabilities**
>
> 9.4.1 CO2 emission per unit of value added

This target is interpreted to cover research about sustainable infrastructure and industry achieved through resource-use efficiency and the adoption of clean and environmentally sound technologies and industrial processes.

See Target 9.1 for details on how we define the concept of infrastructure.

This query consists of one phrase.

#### Phrase 1

This phrase is about the sustainability of infrastructure and industry through resource efficiency and the usage of clean and environmentally friendly technologies and industrial processes. Basic structure is *sustainability + infrastructure/industry + resource-use efficiency /clean technologies / environmentally sound*.

```py
TS=
(
	("sustainab*" OR "renewabl*" OR "resource-efficien*" OR "recyclab*" OR "reusabl*"
	OR "ecofriendly" OR "eco-friendly" OR "environmentally friendly" OR "environmentally sound" OR "ecologically friendly" 
	OR "ecologically sound" OR "low* carbon" 
	OR "green" OR "eco" OR "ecological" OR "nonpollut*" OR "non-pollut*"
	)
	NEAR/5 
	(
		("industry" OR "industries" OR "manufacturer$" OR "industrial sector$"
		OR "infrastruct*" 
		OR (("energy" OR "power") NEAR/1 ("infrastruct*" OR "supply" OR "supplies" OR "solution$" OR "source*")) 
		OR "energy system$" OR "power system$" 
		OR "electrification" OR "electric* transmission" OR "electric* distribution" OR "electric* connections" OR "electric* production" 
		OR "lighting" 
		OR (("waste" OR "wastewater$" OR "sewage") NEAR/1 ("treatment" OR "collection" OR "management")) 
		OR "recycling system$" 
		OR "water suppl*" OR "drinking water" OR "potable water" OR "clean water" OR "sanitation" OR "drainage system$" 
		OR "water and sanitation system$" OR "food suppl*"
		OR "telecommunication$" OR "digital communication$" OR "communication$" OR "digital solution$" OR "internet" OR "mobile network$"
		OR "public amenities" OR "rule of law" OR "juridical system$" OR "legal services" OR "financial service$" OR "banking service$" 
		OR "education" OR "school*" 
		OR "health care" OR "healthcare" 
		OR "buildings" OR "housing" OR "public spaces" OR "disaster management" 
		OR "mass transit*" OR "mobility system$" OR "public transport*" OR "public transit*" OR "transport" OR "transportation" 
		OR "urban mobility" OR "road" OR "roads"
		) 
		NEAR/5
			(
				(("resource$" OR "water" OR "material$" OR "energy") NEAR/1 ("efficien*" OR "sustainable" OR "optimi$ation")) 
				OR "eco-efficien*" OR "circular econom*" OR "circularity" OR "closed-loop economy" 
				OR "industrial ecology" OR "cradle to cradle" OR "cradle-to-cradle"
				OR (("sustainab*" OR "environmental*" OR "ecological*" OR "eco" OR "green" OR "clean" OR "cleaner") NEAR/1 ("technolog*" OR "practice$" OR "production" OR "process*")) 
				OR 
					(
						("footprint" OR "CO2" OR "emission$" 
						OR (("lifecycle$" OR "life-cycle$") NEAR/1 "cost$")
						) 
						NEAR/3 ("decreas*" OR "minimi*" OR "reduc*" OR "restrict*" OR "lower" OR "lower$" OR "lowered")
					)
			)
	)
)
```

### Target 9.5

> **9.5 Enhance scientific research, upgrade the technological capabilities of industrial sectors in all countries, in particular developing countries, including, by 2030, encouraging innovation and substantially increasing the number of research and development workers per 1 million people and public and private research and development spending**
>
> 9.5.1 Research and development expenditure as a proportion of GDP
>
> 9.5.2 Researchers (in full-time equivalent) per million inhabitants

This target is interpreted to cover research on scientific research and the technological capabilities of industrial sectors, including innovation and research and development (R&D) capacity in terms of personnel and funding.

In Target 9.5, we interpret innovation and R&D capacity as the key mechanisms through which scientific research and industrial technological development are advanced, as explicitly stated in the target, and we use these as the basis for our search.

This query consists of one phrase.

#### Phrase 1

This phrase covers scientific research and the technological capabilities of industrial sectors, together with the research and development (R&D) capacity used to advance them. The elements of the phrase are *R&D capacity + scientific research/technological capabilities*.

```py

TS=
(
	("R&D" OR "R & D" OR "R+D" OR "R + D" OR "research and development" OR "research & development" OR "research development and innovation" 
	OR "research and development and innovation" OR "research & development & innovation" OR "research-development-innovation" OR "RDI"
	OR "innovation$"
	OR "worker*" OR "workforce" OR "employee$" OR "staff" OR "labor" OR "labour" OR "job$" OR "researcher$" OR "scientist$"
	OR "invest$" OR "investing" OR "investment$" OR "financ*" OR "fund$" OR "funding" OR "spending*" OR "expend*" OR "expense*" 
	OR "GDP" OR "gross domestic product" OR "incentive$" OR "subsidy" OR "subsidies" OR  "research resource$" OR "technology resource$" OR "technological resource$" 
	OR "financi* resource$" OR "economic resource$" OR "capital resource$" OR "fundamental resource$" OR "science resource$" 
	OR "innovation resource$" OR "knowledge resource$"
	OR "capacity" OR "capabilit*" 
	)
	NEAR/5
		("scientific research" 
		OR (("technological" OR "technology" OR "technologies") NEAR/5 ("industry" OR "industrial*"))
		)
)

```


### Target 9.a

> **9.a Facilitate sustainable and resilient infrastructure development in developing countries through enhanced financial, technological and technical support to African countries, least developed countries, landlocked developing countries and small island developing States**
>
> 9.a.1 Total official international support (official development assistance plus other official flows) to infrastructure

This target is interpreted to cover research about sustainable and resilient infrastructure development in developing countries (African countries, least developed countries, landlocked developing countries and small island developing States) through enhanced financial, technological and technical support (including official development assistance).

This query consists of one phrase. 

#### Phrase 1

This phrase is about sustainable infrastructure development in developing countries through financial or technical support. Basic structure is *sustainable infrastructure + financial/technical support + developing countries*.

```py
TS=
( 
	(
		("reliabl*" OR "sustainab*" OR "resilien*" OR "invulnerab*" OR "adaptab*" OR "flexib*" OR "recoverab*" OR "maintainable*" OR "renewabl*" 
		OR "resource-efficien*" OR "repairab*" OR "recyclab*" OR "reusab*" OR "ecofriendly" OR "eco-friendly" OR "environmentally friendly" 
		OR "environmentally sound" OR "ecologically friendly" OR "ecologically sound" OR "low* carbon" OR "green" OR "eco" OR "ecological" 
		OR "nonpolluting" OR "energy-efficient"
		)  
        NEAR/5 
            ("infrastruct*" 
			OR 
				(("energy" OR "power" OR "electric*") 
				NEAR/1 
					("infrastruct*" OR "supply" OR "supplies" OR "supplying" OR "solution$" OR "source*" OR "transmission" OR "transfer*" OR "distrib*" 
					OR "connections" OR "structure*" OR "foundation"
					)
				) 
			OR "energy system$" OR "power system$" OR "electrification" OR "lighting" 
			OR "waste" OR "wastewater$" OR "sewage" 
			OR "recycling system$" OR "water supply" OR "drinking water" OR "clean water" OR "sanitation" OR "drainage system$" OR "water and sanitation system$" 
			OR "food supply" OR "telecommunication$" OR "digital communication$" OR "communication$" OR "digital solutions" OR "internet" OR "mobile network$" 
			OR "public amenities" OR "rule of law" OR "juridical system$" OR "legal service$" 
			OR "monetary service$" OR "banking service$" 
			OR "education infrastruct*" OR "education system*" OR "school$" OR "health care" OR "healthcare" OR "hospital*" OR "medical care" OR "public service$" 
			OR "buildings" OR "housing" OR "public spaces" OR "sport* facilit*"
			OR "disaster management" OR "disaster prevent*" 
			OR "public alert*" OR "public warn*" OR "early warn*" 
			OR "mass transit*" OR "mobility system$" OR "public transport*" OR "public transit*" OR "rail" OR "rails" OR "railway*" 
			OR "road" OR "roads" OR "transport" OR "transportation" 
			)
	)
	AND
		("financial support" OR "technological support" OR "technical support" 
		OR "official development assistance" OR "ODA" 
		OR "cooperation* fund*" OR "develop* spending*" OR "foreign subsid*" OR "international subsid*" OR "develop* subsid*" 
		OR "humanitar* assist*" OR "humanitar* aid*" OR "humanitar* fund*" OR "humanitar* invest*" 
		OR "cross-national assist*" OR "cross-national aid*" OR "cross-national fund*" OR "cross-national invest*" 
		OR "financial assistance*" OR "financial aid" OR "financial resourc*" OR "financial backing" OR "financial contribution*" 
		OR "financial instrument*" OR "monetary support*" OR "economic support*" OR "external support*"
		OR "technolog* transfer*" OR "transfer of technical knowledge" OR "transfer of technolog*" OR "technical assistance" OR "capacity building"
		OR "multilateral development bank*" OR "development bank*"
		OR "development aid" OR "development assistan*" OR "development financ*" OR "development fund*"
		OR (("foreign" OR "international" OR "donor*" OR "multilateral" OR "bilateral") NEAR/3 ("invest*" OR "financ*" OR "fund*" OR "support*" OR "assist*" OR "aid"))
		)
    AND 
		("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world" 
		OR "less developed countr*" OR "less developed nation$" 
		OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$" OR "underserved countr*" OR "underserved nation$" 
		OR "deprived countr*" OR "deprived nation$" OR "middle income countr*" OR "middle income nation$" 
		OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$" 
		OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$" OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" 
		OR "transitional countr*" OR "emerging economies" OR "emerging nation$" 
		OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" 
		OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" 
		OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" 
		OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" 
		OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" 
		OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" 
		OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" 
		OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*" 
		OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" 
		OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" 
		OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" 
		OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" 
		OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" 
		OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" 
		OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" 
		OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" 
		OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" 
		OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands" OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" 
		OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" 
		OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" 
		OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" 
		OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" 
		OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*" 
		)    
) 
 
```

### Target 9.b

> **9.b Support domestic technology development, research and innovation in developing countries, including by ensuring a conducive policy environment for, inter alia, industrial diversification and value addition to commodities**
>
> 9.b.1 Proportion of medium and high-tech industry value added in total value added

This target is interpreted to cover research about domestic technology development, research and innovation in developing countries.

This query consists of one phrase. 

#### Phrase 1

This phrase is about domestic technology development, research and innovation in developing countries. Basic structure is *domestic + research, development and innovation + developing countries*. 

```py

TS=
(
	("domestic" OR "national*" OR "local*")
	NEAR/5
		("research and development" OR "R&D" OR "research & development" OR "research and innovation" 
		OR (("technolog*" OR "innovation$") NEAR/3 ("capacity building" OR "capacity development"))
		OR (("technolog*" OR "innovation$") NEAR/3 ("policy" OR "policies" OR "capacit*" OR "capabilit*" OR "transfer" OR "upgrading" OR "development"))
		OR "industrial diversification" OR "innovation system$" OR "innovation ecosystem*" OR "innovation$"
		OR "value addition" OR "addition of value" OR "value added"
		OR "industrial technology" OR "triple helix" OR "industrial polic*"
		)	
   	NEAR/10
		("least developed countr*" OR "least developed nation$" OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world" 
		OR "less developed countr*" OR "less developed nation$" 
		OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$" OR "underserved countr*" OR "underserved nation$" 
		OR "deprived countr*" OR "deprived nation$" OR "middle income countr*" OR "middle income nation$" 
		OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$" 
		OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$" OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" 
		OR "transitional countr*" OR "emerging economies" OR "emerging nation$" 
		OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" 
		OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" 
		OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" 
		OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" 
		OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" 
		OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" 
		OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" 
		OR "Nepal*" OR "Yemen*" OR "Haiti*" OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" 
		OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" 
		OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" 
		OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" 
		OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" 
		OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" 
		OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" 
		OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" 
		OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" 
		OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands" OR "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" 
		OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" 
		OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" 
		OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" 
		OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" 
		OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*" 
		OR "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" 
		OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" 
		OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" 
		OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" 
		OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" 
		OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" 
		OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" 
		OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" 
		OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" 
		OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" 
		OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" 
		OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" 
		OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" 
		OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" 
		OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" 
		OR "turkish" OR "turkey" OR "georgia*"
		)
) 

```

### Target 9.c

> **9.c Significantly increase access to information and communications technology and strive to provide universal and affordable access to the Internet in least developed countries by 2020**
>
> 9.c.1 Proportion of population covered by a mobile network, by technology

This target is interpreted to cover research about access to information and communications technology in least developed countries and providing universal and affordable access to the Internet in least developed countries.

This query consists of one phrase. 

#### Phrase 1

This phrase is about access to information and communications technology in least developed countries. Basic structure is *access/barriers + ITC + least developed countries*.
 

```py
TS=
(
	(
		(
			("access*" OR "equitab*" OR "inequitab*" OR "equity" OR "equality" OR "equal" 
			OR "afford*" OR "low cost" OR "inexpensive*" OR "reasonable" OR "connectiv*" OR "provide" OR "provides" OR "providi*" OR "enabl*"
			OR "barrier$" OR "obstacle$" OR "inequal*" OR "unequal" OR "expensive*" OR "unaffordab*" OR "costly" OR "high-price$" OR "high price$"
			)
			NEAR/15
				("Internet" OR "internet access*" OR "internet connectiv*" OR "internet connection*"
				OR "mobile network" OR "mobile broadband" OR "basic mobile network" OR "mobile connectiv*" 
				OR "information technolog*" OR "communication technolog*" OR "ICT" OR "information and communication$ technolog*" OR "information & communication$ technolog*" 
				OR "information communication$ technolog*" 
				OR "digital infrastructure" OR "telecommunication*" OR "telecom network" OR "broadband" OR "telecom system*"
				OR "wireless network" OR "wireless broadband" OR "wifi" OR "wireless technologies" 
				OR "2G" OR "3G" OR "4G" OR "5G" OR "LTE"
				)
		)
		OR ("digital divide" OR "digital inclusion")
	)
	NEAR/20 
		("least developed countr*" OR "least developed nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" 
		OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" 
		OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" 
		OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" 
		OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" 
		OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
		) 
) 

```

## 4. Contributions

* v2.1.0: Taina Peltonen, Johanna Löhönen (March 2026)

* Internal review: Paula Nissilä (December 2025)

Specialist input: Eeva-Liisa Viskari (Chief Specialist in Sustainability and ESG) Tampere University (December 2025)

## 5. Footnotes

<span id="f4">Soriano, A, Gaikwad S, Stratton-Short S, Bajpai A, Imbuye J. (2022).</span> *Inclusive infrastructure for climate action*. UNOPS, Copenhagen, Denmark. Available https://wrd.unwomen.org/sites/default/files/2023-03/Inclusive_Infrastructure_Climate_Action.pdf [Accessed 2025.07.07]

<span id="f2">United Nations. (2016, 2017, 2018, 2019, 2020, 2021).</span> *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

<span id="f7">United Nations Department of Economic and Social Affairs. (2023).</span> *Accounting for Global Value Chains: GVC Satellite Accounts and Integrated Business Statistics*. United Nations. https://unstats.un.org/unsd/business-stat/GVC/Accounting_for_GVC_web.pdf [Accessed 2025-11-12]

<span id="f8">United Nations Environment Programme. (2021).</span> *International Good Practice Principles for Sustainable Infrastructure*. Nairobi Available https://wedocs.unep.org/bitstream/handle/20.500.11822/34853/GPSI.pdf [Accessed 2025.07.08]

<span id="f9">United Nations Industrial Development Organization. (2013).</span> *Lima Declaration: Towards Inclusive and Sustainable Industrial Development*. General Conference Resolution GC.15/Res.1. Lima, Peru: UNIDO, 2013. Available: https://www.unido.org [Accessed 9.7.2025]

<span id="f10">United Nations Industrial Development Organization. (2021).</span> *Industrial Development Report 2022*. The Future of Industrialization in a Post-Pandemic World. Vienna. https://digitallibrary.un.org/record/3994233?v=pdf [Accessed 9.7.2025]

<span id="f1">UN DESA. (2025).</span> *Goals: Build resilient infrastructure, promote inclusive and sustainable industrialization and foster innovation*. https://sdgs.un.org/goals/goal9#targets_and_indicators [Accessed 2025.04.02]

<span id="f3">UN Statistics Division. (2025).</span> *SDG indicator metadata [9.3.1]* https://unstats.un.org/sdgs/metadata/files/Metadata-09-03-01.pdf [Accessed 2025-11-11]

<span id="f5">World Bank. (2020). </span> *World Development Report 2020: Trading for Development in the Age of Global Value Chains*. Washington, DC: World Bank. doi:10.1596/978-1-4648-1457-0. https://digitallibrary.un.org/record/3850531/files/9781464814570.pdf