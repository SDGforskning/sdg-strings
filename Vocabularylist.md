# Vocabulary reference list

Lists of potential search terms for themes/actions commonly referred to in the SDG targets/indicators. This list is to be referred to under query construction as an aid. The list does not include subject-specific vocabulary - see notes on the individual SDG queries.

The names for each section reflect an approximate theme of the search terms within.

Not all possible terms from this list must be included in the search queries every time the theme is mentioned, as not all will be appropriate in all contexts. Wildcards and truncation used in this list is not prescriptive (i.e. it may have to be altered or other forms of the words added in the queries, depending on context).

## SDGs and/or sustainability

Note: Web of Science reads "SDG-1" also as "SDG 1"

```Ceylon=
"SDG1"
"SDG 1"
"sustainable development goal$ 1"
 (("sustainable development goal$" OR "SDG$" OR "goal 1")  NEAR/15 "poverty")

#More general
"sustainable development"
"sustainab*"
"eco-friendly"
```

## Countries

Lists of least developed countries, small island developing states and landlocked developing states are from the United Nations World Economic Situation and Prospects (tables F, H and I, pages 173-174) - United Nations (2019) World Economic Situation and Prospects (Statistical Annex). https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/

```Ceylon=
#General terms
(("least developed" OR "developing" ) NEAR/3 ("countr*" OR "state$" OR "nation$"))
"developing world"
"official development assistance"
"official development aid"
"international aid"

#Least developed Countries (LDCs)
"Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"

#Small island developing states (SIDS)
"Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands"

#Landlocked developing states (LDS)
"Afghanistan" OR "Armenia" OR "Azerbaijan" OR "Bhutan" OR "Bolivia" OR "Botswana" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "Ethiopia" OR "Kazakhstan" OR "Kyrgystan" OR "Lao People’s Democratic Republic" OR "Lesotho" OR "Malawi" OR "Mali" OR "Mongolia" OR "Nepal" OR "Niger" OR "Paraguay" OR "Republic of Moldova" OR "Rwanda" OR "South Sudan" OR "Tajikistan" OR "The former Yugoslav Republic of Macedonia" OR "Turkmenistan" OR "Uganda" OR "Uzbekistan" OR "Zambia" OR "Zimbabwe"
```

## Groups of people

Note that `poor` or e.g. `old` cannot be used alone (adjecitve).

```Ceylon=
"the poor"
"the poorest"
"rural poor"
"urban poor"
(("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*"))

"the vulnerable"
"vulnerable group$"

("person$" OR "people" OR "adult$")
    NEAR/3 ("disabled" OR "disabilities" OR "unemployed" OR "older" OR "elderly")
"disability"

("person$" OR "people" OR "adult$")
    NEAR/3 ("unemployed")

"patient$"

("person$" OR "people" OR "adult$")
    NEAR/3 ("older" OR "elderly")
"old* person$"
"old* people"
"elderly"

"pregnant"
"pregnancy"
"fetus" OR "foetus" OR "fetal" OR "foetal"
"perinatal" OR "prenatal" "neonatal" OR "antenatal"
"newborn$"
"babies"
"infant$"
"newborn$"
"children"
"child"
"under-five"
"girls"
"boys"

"adult$"
"women" OR "woman"
"men" OR "man"

"humans" OR "humanity" OR "human"
"people" OR "person$"

"rural"
"urban" OR "city" OR "cities" OR "town$" OR "village$"
"countr*" OR "nation$" OR "develop* state$"
```

## Effects

```Ceylon=
"impact$"
"effect$"
"affect$"
"affecting"
"affected"
"response$"
"consequence$"
```

## Actions

### Improving/increasing

```Ceylon=
"increas*"
"strengthen*"
"improv*"
"restor*"
"enhanc*"
"better"
"more efficient"
"higher"
"upgrad*"
"overcome"
```

### Maintaining/conserving

```Ceylon=
"maintain*"
"conserv*"
"preserv*"
```

### Decreasing

Truncate `limit` carefully (suggestion: `limit$` - limitations used often with unrelated meaning)

`tackle*`, `fight` and `combat` have multiple meanings (metaphorical)

```Ceylon=
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
```

### Ending or preventing

Truncate `end` carefully (e.g. endometriosis, endotherm).

`combat` has multiple meanings (metaphorical)

```Ceylon=
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
```

### Adapting or coping

Truncate `cope` carefully (e.g. copepod)

```Ceylon=
"coping"
"cope"
"adapt*"
"resilien*"
"mitigat*"
"preparedness"
"risk reduction"
```

### Managing/legislating

Truncate `polic*` and `program*` carefully (e.g. police, programmers)

```Ceylon=
"manag*"
"prohibit*"
"regulat*"
"legislat*"
"govern*"
"strateg*"
"polic*"
"legal*"
"law$"
"framework$"
"risk reduction"
"preparedness"
"planning"
"service$"
"agenc*"
"program*"
```

### Assessing

```Ceylon=
"assess*"
"examin*"
"evaluat*"
"measur*"
"monitor*"
```

### Establishing

Truncate `plan` carefully (e.g. planes)

```Ceylon=
"establish*"
"propose*"
"design*"
"implement*"
"plan"
"plans"
"planned"
"planning"
"adopt*"
"build*"
```

### Treating

Truncate `cure` carefully

```Ceylon=
"treat*"
"remediat*"
"correct*"
"cleanup"
"alleviat*"
"cure"
"cured"
"rehabilitat*"
```

## Security/insecurity

```Ceylon=
"securing"
"secure" / "insecure"
"secures"
"security" / "insecurity"
"ensur*"
"protect*" / "unprotect*"
"conserv*"
"preserv*"
"reliab*" / "unrelaib*"
"vulnerab*"
"stability"

"preparedness"
"early warning"
```

## Access and sharing

`equity`, `justice`, `democracy` may need combining in a phrase (e.g. `health equity`, `energy democracy`)

```Ceylon=
"equitab*" / "inequitab*"
"equity"
"equality" / "inequality"
"equal" / "unequal"
"share"
"sharing"
"shared benefit$" OR "benefit sharing"
"justice"
"democracy"

"affordab*" / "inaffordab*"

"right$"
"ownership"
"access*"
"control"

"barrier$"
"obstacle$"
```

## Capacity and technology transfer

From United Nations Development Group (2017) Capacity Development, UNDAF companion guidance. https://unsdg.un.org/resources/capacity-development-undaf-companion-guidance [accessed 19.12.2019]:

* Definition of "capacity" : "[...] the ability of people, organizations and society as a whole to manage their affairs successfully".
* Definition of "capacity development" : "the process whereby people, organizations and society as a whole unleash, strengthen, create, adapt, and maintain capacity over time, in order to achieve development results".

```Ceylon=
"framework$"
"capacity"
"capabilit*"
"infrastructure"
"facilities"
"network$"
"initiative$"
"international cooperation"
"international collaboration"
"technical knowledge transfer*"
"transfer of technical knowledge"
"transfer of technolog*"
"capacity building" OR "capacity development"
```

## Climate changes

See also "Risks and disasters". For more terms (GHG, climate mitigation etc.), see SDG13 string.

```Ceylon=
"climate change"
"climatic change$"
"global warming"
"changing climate"
("climate" OR "atmospher*" OR "ocean") NEAR/3 "warming")
("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
```

## Risks and disasters

```Ceylon=
"disaster$"
"catastrophe$"
"risk$"
"shock$"
"hazard*"
"collaps*"

"tipping point$"
"extrem*"
("extreme$" NEAR/2 ("climat*" OR "weather" OR "precipitation"))
"drought$"
"flood*"

"financial crash*"
"economic downturn$"

"disaster risk reduction"
"Sendai Framework for Disaster Risk Reduction"
"preparedness"
"early warning"
"protect*"
```

## Financial assistance, investment and income

Truncate `invest` and `subsidy` carefully (e.g. investigated, subside)

```Ceylon=
"incentive$"
"subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
"government* subsid*"
"economic subsid*"
"price support$"
"tax break$"

"market$"
"investment$"
"investing"
"invest"
"financ*"

"ODA" OR "official development assistance"
"official development aid"
"foreign aid"
"international aid"
"cooperation fund"

"income$"
"wage$"
"pay"
"money"
"econom*"
"GDP"
```

## Social/welfare services

```Ceylon=
"social protection$"
"social floor$"
"social service$"
"welfare system$"
"welfare service$"
"social welfare"
"social security"

"basic service$"
"essential service$"
```

## Feasibility/adoption/uptake of a new technology

```Ceylon=
"barrier$"
"obstacle$"
"implement*"
"adopt*"

"subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
"government* subsid*"
"economic subsid*"
"price support$"
"tax break$"
"incentive$"
"economic feasibility"
"cost-effectiveness"
"affordab*"
"cost-advantage$"

"upscale" OR "scale-up"
"commercial development"
"develop* commercially"
"commerciali?ation"
```
