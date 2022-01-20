# Search query for SDG 14 - Life below water, Bergen topic-approach.

***Current status**: Not under active development, awaiting the action approaches to be finished. Similar to the original version (v2019.11).* 

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 14
3. Marine terms: String for limiting certain phrases to the marine environment
4. Documentation and string sections for each target

## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 14</summary>

  
  Note that this query should be run in multiple steps, and then combined as shown in the final steps.

  Search #1
  ```
TS= ( "ocean$" OR "oceanogra*" OR "marine" OR "seas" OR "deep sea" OR "seabed" OR "seamount$" OR "hydrothermal vent$" OR "cold seep$" OR "organic fall$" OR "bathyal" OR "abyssal" OR "submarine" OR "subtidal" OR "intertidal" OR "rocky shore$" OR "mangrove$" OR "kelp bed$" OR "kelp forest$" OR (("seaweed$" OR "macroalga*") NEAR/3 ("bed$" OR "assemblage$" OR "communit*")) OR "seagrass*" OR "beach*" OR "salt marsh*" OR "mud flat$" OR "*tidal flat" OR "*tidal flats" OR "sea ice" OR "sponge ground$" OR "reef" OR "reefs" OR "estuar*" OR "fjord$" OR "coastal habitat$" OR "coastal ecosystem$" OR "coastal communit*" OR "coastal water$" OR "coastal dune$" OR "coastal zone management" OR (("coast*" OR "*tidal") NEAR/15 ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$" OR "offshore" OR "fish*" OR "aquaculture" OR "shrimp farm*")) OR ("sea" NEAR/15 ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$" OR "offshore" OR "*tidal" OR "fish*" OR "aquaculture" OR "shrimp farm*")) OR (("harbour$" OR "port" OR "ports") NEAR/15 ("sea" OR "seas" OR "coast*" OR "gulf" OR "ship*" OR "maritime")) ) OR SO=( ("marine*" OR "ocean*" OR "estuar*" OR "deep sea*") OR ("Annual review of marine*" OR "Advances in marine*" OR "African journal of marine*" OR "Archive of fishery and marine*" OR "Biologiya moray marine*" OR "Bulletin of marine*" OR "Cahiers de biologie marine*" OR "Frontiers in marine*" OR "Geo marine*" OR "Helgoland marine*" OR "ICES journal of marine*" OR "Indian journal of marine*" OR "International journal of marine*" OR "Journal of experimental marine*" OR "Journal of marine*" OR "Meeresforschung reports on marine*" OR "mer marine*" OR "molecular marine*" OR "Regional studies in marine*" OR "Research in marine*" OR "Russian journal of marine*" OR "South African journal of marine*" OR "Transnav international journal on marine*" OR "Vie et milieu serie a biologie marine*" OR "Applied ocean*" OR "China ocean*" OR "Acta ocean*" OR "Annales de l institut ocean*" OR "Applied ocean*" OR "Brazilian journal of ocean*" OR "Cahiers orstom ocean*" OR "California cooperative ocean*" OR "Fisheries ocean*" OR "Fishery bulletin of the national ocean*" OR "IEEE journal of ocean*" OR "International journal of naval architecture and ocean*" OR "Journal of geophysical research ocean*" OR "Journal of ocean*" OR "Journal of operational ocean*" OR "Journal of physical ocean*" OR "Journal of the waterway port coastal and ocean*" OR "Physical ocean*" OR "Progress in ocean*" OR "Revista de biologia marina y ocean*" OR "Vie et milieu serie b ocean*" ) )
  ```
  Search #2
  ```
TS=( ( ( "pollut*" OR "wastewater" OR "eutrophicat*" OR (("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*") NEAR/15 ("waste" OR "effluent$" OR "runoff" OR "eutrophicat*" OR "ecotox*")) OR "oil spill$" OR "litter" OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*")) OR "plastic$" OR "microplastic$" OR (("heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT") NEAR/15 ("contamina*" OR "bioaccumula*")) OR "noise pollution" OR (("mine tailings" OR "mining") NEAR/15 ("contam*")) ) ) NOT ("PM2.5" OR "PM10") )
  ```
  Search #3
  ```
TS=( ( (("ecosystem-based" OR "area-based") NEAR/3 ("manag*" OR "approach*" OR "govern*")) OR ("sustainab*" NEAR/3 ("manag*" OR "govern*")) OR "marine spatial planning" OR "spatial management" OR "coastal zone management" OR "locally managed marine area$" OR "LMMA$" OR "ecosystem restoration" OR "habitat restoration" ) OR (("manag*" OR "protect*" OR "conserv*") NEAR/15 ("resilien*" OR "biodiversity" OR ("ocean$" NEAR/3 "health$") OR ("ecosystem$" NEAR/3 "health$") ) ) OR ( (("protect*" NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$")) OR ("no-take" NEAR/3 ("area*" OR "zone*")) ) ) )
  ```
  Search #4
  ```
TS=( ("acidif*" NEAR/15 ("ocean$" OR "seawater" OR "sea water" OR "marine") ) AND ("impact*" OR "effect$" OR "affect$" OR "response$" OR "consequence$" OR "calcif*" OR "decalcif*" OR "calcium carbonate" OR "dissol*" OR "aragonite" OR "calcite" ) )
  ```
  Search #5
  ```
TS= ( ("overfish*" OR (("overharvest*" OR "overexploit*") NEAR/15 ("fish*" OR "shellfish*")) OR "bycatch" OR "by-catch" OR (("illegal*" OR "unreport*" OR "unregulated" OR "destructive" OR "blast" OR "dynamite" OR "ghost" OR (("gear" OR "tackle") NEAR/5 ("abandoned" OR "lost" OR "discarded")) ) NEAR/10 ("fishing" OR "fisher*" OR "trawl*" OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*")) ) ) ) OR (("fishery" OR "fisheries" OR "fishing" OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*")) OR "fish stock$" OR ("catch" NEAR/3 ("entitlement" OR "limit$" OR "tolerance$")) ) AND ("manage*" OR "restor*" OR "protect*" OR "conservation" OR "sustainab*" OR "assess*" OR "collaps*" OR "maximum sustainable yield*" OR "MSY" OR "marine stewardship council" OR "regional fisheries managment organi?ation$" OR "RFMOs" OR "UNCLOS" OR "convention on the law of the sea" OR "fish stocks agreement" OR "code of conduct for responsible fisheries" OR "CCRF" OR "port state measures agreement" ) ) )
  ```
  Search #6
  ```
TS= ( ( ("MPA" OR "MPAs" OR "marine protected area$" OR "reserve" OR "reserves" OR "marine park$" OR "marine conservation zone$" OR (("protected" OR "protection") NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$")) OR (("conserved" OR "conservation" OR "conserves" OR "conserving") NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$")) OR ("no-take" NEAR/3 ("area*" OR "zone*")) OR "conservation action$" ) ) OR (("biodivers*" OR "biological diversity") NEAR/3 ("beyond national jurisdiction" OR "beyond areas of national jurisdiction" OR "ABNJ")) OR "BBNJ" )
  ```
  Search #7
  ```
TS=( ( ("overfish*" OR (("overharvest*" OR "overexploit*") NEAR/15 ("fish*" OR "shellfish*" OR "stock$")) OR "bycatch" OR "by-catch" OR( ("illegal*" OR "unreport*" OR "unregulated" OR "destructive" OR "blast" OR "dynamite" OR "ghost" OR (("gear" OR "tackle") NEAR/5 ("abandoned" OR "lost" OR "discarded")) OR "overcapacity" ) NEAR/15 ("fishing" OR "fisher*" OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*")) ) ) ) OR ( (("developing" OR "least developed") NEAR/3 ("state*" OR "nation$" OR "countr*") ) OR "developing world" OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands" ) ) AND ( ("ODA" OR "official development assistance" OR "world trade organisation" OR "WTO" OR "government* subsid*" OR "economic subsid*" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e" OR "price support$" OR "tax break$" ) AND ("fishing" OR "fisher*" OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*")) ) ) )
  ```
  Search #8
  ```
TS=( ( ("sustainab*" NEAR/15 ("tourism" OR "ecotourism" OR "tourist$" OR "whale watch*" OR "sightsee*" OR "recreation*" OR "aquaculture" OR "fish farm*" OR "fisher*" OR "fishing" OR "harvest*" OR "exploit*" OR "use" OR "using" OR "manag*" OR "livelihood$" OR "social-ecological system$" OR "socialecological system$" OR "econom*" ) ) OR "bio-econom*" OR "bioeconom*" OR "blue growth" OR "blue econom*" OR "blue bond$" OR (("marine spatial planning" OR "ecosystem based management") AND "econom*") ) AND ( (("least developed") NEAR/3 ("state*" OR "nation$" OR "countr*" OR "small island*" OR "Pacific island*") ) OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands" ) )
  ```
  Search #9
  ```
TS=( ( ("blue growth" OR "blue econom*" OR "blue bond$" OR "bioprospect*" OR "biopiracy" OR ("bioactive" NEAR/3 ("compound*" OR "substance*")) OR "bioresource$" OR "biological resource$" OR "genetic resource$" OR "biotechnolog*" OR (("biodivers*" OR "diversity") NEAR/15 ( "development" OR "livelihood$" OR "fisher*" OR "fishing" OR "harvest*" OR "tourism" OR "ecotourism" OR "tourist$" OR ("ecosystem*" NEAR/3 "service$") OR "Nagoya protocol" ) ) ) AND ( (("developing" OR "least developed") NEAR/3 ("state*" OR "nation$" OR "countr*" OR "small island*" OR "Pacific island*") ) OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti" OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands" ) ) OR ("transfer of marine technolog*" OR "marine technology transfer") OR ( (("share$" or "sharing" OR "develop*" OR "establish*" OR "increas*" OR "improv*" OR "build*" OR "implement*" OR "capacity development" OR "develop* capacity" OR "invest" OR "investment$" OR "investing" OR "joint research" OR "joint effort$" OR "collaborat*" OR "international cooperation" ) AND ( (("research" OR "scientific" OR "science") NEAR/5 ("policy" OR "policies" OR "programme$" OR "advisor$" OR "framework$" OR "initiative$" OR "capacity" OR "capabilit*" OR "infrastructure" OR "facilities" OR "vessel$" OR "vehicle$" OR"network$") ) OR "observ* network$" OR "observ* system$" OR "data infrastructure$" OR "data network$" OR "monitoring network$" OR "ecological monitoring" OR (("ocean*" OR "marine" OR "biological") NEAR/2 ("observator*" OR "monitoring")) OR (("taxonom*" OR "genom*" OR "species") NEAR/5 ("knowledge" OR "research" OR "capacity" OR "compentence$" OR "database$" OR "register$" OR "inventory" OR "inventories") ) ) ) AND ("biodiversity" OR ("biological" NEAR/3 "diversity") OR (("ocean*" OR "marine") NEAR/3 ("research" OR "science")) OR "ocean health" OR "ecosystem health" OR "healthy ocean$" ) ) )
  ```
  Search #10
  ```
TS=( ( ("fisher*" OR "fishing" OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*")) ) NEAR/5 ("small-scale" OR "artisan*" OR "tradition*" OR "subsistence" ) ) AND ( ("access*" OR "use* right$" OR "ownership" OR "control$" OR "equitab*" OR "inequitab*") ) )
  ```
  Search #11
  ```
TS=( ("conserv*" OR "blue growth" OR ("sustainab*" NEAR/15 ("use" OR "exploit*" OR "manag*" OR "govern*" OR "fisher*" OR "fishing" OR "harvest*" OR "tourism" OR "ecotourism" OR "tourist$" OR "aquaculture" OR "fish farm*" OR "resource$" OR "economy" ) ) ) AND ("law of the sea" OR "UNCLOS" OR "the future we want" OR (("biodivers*" OR "biological diversity") NEAR/3 ("beyond national jurisdiction" OR "ABNJ")) OR "BBNJ" OR "common fisheries policy" OR "deep-sea fisheries guidelines" OR "Management of Deep-sea Fisheries in the High Seas" OR ("convention$" NEAR/3 ("Conservation of Antarctic Living Marine Resources" OR "biological diversity" OR "OSPAR")) OR "MSFD" OR ("directive$" NEAR/3 ("marine strategy framework" OR "water framework" OR "marine spatial planning")) OR ("international" NEAR/3 ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" ) ) ) )
  ```
  Search #12
  ```
TS= ("SDG14" OR "SDG 14" OR "SDG-14" OR "sustainable development goal$ 14" OR (("sustainable development goal$" OR "SDG$" OR "goal 14") AND "Life below water") OR (("sustainable development goal$" OR "SDG$" OR "goal 14") NEAR/15 "oceans"))
  ```
  Search #13
  ```
#2 OR #3 OR #4 OR #6 OR #8 OR #9 OR #11
  ```
  Search #14
  ```
#1 AND #13
  ```
  Search #15
  ```
#5 OR #7 OR #10 OR #12 OR #14
  ```

</details>

## 2. General notes

Source of Targets and Indicators:
Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] <sup id="SDGT+Is">[1](#f1)</sup>

Lists of least developed countries, small island developing states and landlocked developing states are from the United Nations World Economic Situation and Prospects (tables F, H and I, pages 173-174)<sup id="UNLDCs">[2](#f2)</sup>.


## 3. Marine terms: String for limiting certain phrases to the marine environment

This query is referred to as **marine terms**, and should be combined with various other sets with `AND` (when instructed) to limit the results to the marine environment. It is not combined with fishery targets, as the results become too limited (many fisheries papers do not use these words, or concern both freshwater and marine fisheries).

The first part (`TS=`) consists of marine habitats, organisms, physical features, and terms to do with the coast. The second part (`SO=`) consists of marine journal titles. Journal name is used as not all publications use marine words in their abstract, title or keywords (e.g. if they are discussing a specifc marine species for an audience who knows it is marine). Journals with over 100 articles are included, but not if Freshwater or Atmospheric elements are in their title. List gathered from Publication Name Index in Web of Science (in searches for “marine*” or “ocean*”).

`seaweed$` and `macroalga*` are combined with other terms to prevent inclusion based on mentions of seaweeds (e.g. seaweed extracts used in industrial processes). `coast` and `sea` are combined with other terms to prevent hits that are not really about the ocean (e.g. terrestrial work in "Mediterranean Sea countries").

```Ceylon =
TS=
(
  "ocean$" OR "oceanogra*"
  OR "marine" OR "submarine"
  OR "seas"
  OR "seabed"
  OR "seamount$"
  OR "hydrothermal vent$" OR "cold seep$"
  OR "subtidal" OR "intertidal" OR "deep sea" OR "bathyal" OR "abyssal"
  OR "rocky shore$" OR "beach*"
  OR "salt marsh*" OR "mud flat$" OR "*tidal flat" OR "*tidal flats"
  OR "estuar*" OR "fjord$"
  OR "sea ice"

  OR "mangrove$"
  OR "kelp bed$" OR "kelp forest$"
  OR (("seaweed$" OR "macroalga*") NEAR/3 ("bed$" OR "assemblage$" OR "communit*"))
  OR "seagrass*"
  OR "sponge ground$" OR "organic fall$"
  OR "reef" OR "reefs"  

  OR "coastal habitat$" OR "coastal ecosystem$" OR "coastal dune$" OR "coastal water$"
  OR "coastal communit*" OR "coastal zone management"
  OR (
      ("coast*" OR "*tidal")
      NEAR/15
          ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$" OR "offshore"
            OR "fish*" OR "aquaculture" OR "shrimp farm*"
          )
     )
     OR (
         ("sea")
         NEAR/15
             ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$" OR "offshore" OR "*tidal"
               OR "fish*" OR "aquaculture" OR "shrimp farm*"
             )
        )
      OR (
          ("harbour$" OR "port" OR "ports")
          NEAR/15
              ("sea" OR "seas" OR "coast*" OR "gulf" OR "ship*" OR "maritime")
         )
)

OR

SO =
(
  "marine*" OR "ocean*" OR "estuar*" OR "deep sea*"
  OR "Annual review of marine*"
  OR "Advances in marine*"
  OR "African journal of marine*"
  OR "Archive of fishery and marine*"
  OR "Biologiya moray marine*"
  OR "Bulletin of marine*"
  OR "Cahiers de biologie marine*"
  OR "Frontiers in marine*"
  OR "Geo marine*"
  OR "Helgoland marine*"
  OR "ICES journal of marine*"
  OR "Indian journal of marine*"
  OR "International journal of marine*"
  OR "Journal of experimental marine*"
  OR "Journal of marine*"
  OR "Meeresforschung reports on marine*"
  OR "mer marine*"
  OR "molecular marine*"
  OR "Regional studies in marine*"
  OR "Research in marine*"
  OR "Russian journal of marine*"
  OR "South African journal of marine*"
  OR "Transnav international journal on marine*"
  OR "Vie et milieu serie a biologie marine*"
  OR "Applied ocean*"
  OR "China ocean*"
  OR "Acta ocean*"
  OR "Annales de l institut ocean*"
  OR "Applied ocean*"
  OR "Brazilian journal of ocean*"
  OR "Cahiers orstom ocean*"
  OR "California cooperative ocean*"
  OR "Fisheries ocean*"
  OR "Fishery bulletin of the national ocean*"
  OR "IEEE journal of ocean*"
  OR "International journal of naval architecture and ocean*"
  OR "Journal of geophysical research ocean*"
  OR "Journal of ocean*"
  OR "Journal of operational ocean*"
  OR "Journal of physical ocean*"
  OR "Journal of the waterway port coastal and ocean*"
  OR "Physical ocean*"
  OR "Progress in ocean*"
  OR "Revista de biologia marina y ocean*"
  OR "Vie et milieu serie b ocean*"
)

```

## 4. Targets

## Target 14.1

> **14.1 By 2025, prevent and significantly reduce marine pollution of all kinds, in particular from land-based activities, including marine debris and nutrient pollution**
>
> 14.1.1 (a) Index of coastal eutrophication; and (b) plastic debris density

This query consists of 1 phrase. **It should be combined with marine terms with `AND`**

The `NOT PM.2.5 OR PM10` expression at the end was included to remove aspects of atmospheric pollution which can include terms for coast but are not really marine.

```Ceylon =
TS=
(
    (  "pollut*"
    OR "wastewater"
    OR "eutrophicat*"
    OR
      (
        ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*")
        NEAR/15
            ("waste" OR "effluent$" OR "runoff" OR "eutrophicat*" OR "ecotox*")          
      )
    OR "oil spill$"
    OR "litter"
    OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
    OR "plastic$" OR "microplastic$"
    OR
      (
        ("heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT")
        NEAR/15
            ("contamina*" OR "bioaccumula*")          
      )
    OR (("mine tailings" OR "mining") NEAR/5 ("contam*"))
    OR "noise pollution"
    )
  NOT ("PM2.5" OR "PM10")
)

```

## Target 14.2

> **14.2 By 2020, sustainably manage and protect marine and coastal ecosystems to avoid significant adverse impacts, including by strengthening their resilience, and take action for their restoration in order to achieve healthy and productive oceans**
>
> 14.2.1 Number of countries using ecosystem-based approaches to managing marine areas

This query consists of 3 phrases. **All should be combined with marine terms with `AND`**

##### Phrase 1:

These terms are included without action terms, as management is already inherent.

```Ceylon =
TS=
(
      (("ecosystem-based" OR "area-based") NEAR/3 ("manag*" OR "approach*" OR "govern*"))
  OR  (("sustainab*") NEAR/3 ("manag*" OR "govern*"))
  OR "marine spatial planning" OR "spatial management"
  OR "coastal zone management"
  OR "locally managed marine area$" OR "LMMA$"
  OR "ecosystem restoration" OR "habitat restoration"
)

```

##### Phrase 2:

```Ceylon =
TS=
(
  ("manag*" OR "protect*" OR "conserv*")
  NEAR/15
    ("resilien*"
    OR "biodiversity"
    OR ("ocean$" NEAR/3 "health$")
    OR ("ecosystem$" NEAR/3 "health$")  
    )
)
```

##### Phrase 3:

Combined to get results which are actually discussing the management/establishment/impacts of protected areas

```Ceylon =
TS=
(
    ("protect*" NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$"))
    OR ("no-take" NEAR/3 ("area*" OR "zone*"))
)

```

## Target 14.3

> **14.3 Minimize and address the impacts of ocean acidification, including through enhanced scientific cooperation at all levels**
>
> 14.3.1 Average marine acidity (pH) measured at agreed suite of representative sampling stations

This query consists of 1 phrase. **It should be combined with marine terms with `AND`**

The target has a clear focus on impacts, therefore this is the focus of this query. Focus on impacts by combining with "impact" words and calcification terms, as this is specifically affected by acidification.

Topic approach: `NEAR` is changed to `AND`

``` Ceylon =
TS =
(
  ("acidif*" NEAR/15 ("ocean$" OR "seawater" OR "sea water" OR "marine")
  AND
      ("impact*" OR "effect$" OR "affect$" OR "response$" OR "consequence$"
      OR  "calcif*" OR "decalcif*" OR "calcium carbonate" OR "dissol*" OR "aragonite" OR "calcite"
      )
)

```   

## Target 14.4

> **14.4 By 2020, effectively regulate harvesting and end overfishing, illegal, unreported and unregulated fishing and destructive fishing practices and implement science-based management plans, in order to restore fish stocks in the shortest time feasible, at least to levels that can produce maximum sustainable yield as determined by their biological characteristics**
>
> 14.4.1 Proportion of fish stocks within biologically sustainable levels

This query consists of 2 phrases.

##### Phrase 1:

Relevant legislation and organisations to reducing overfishing included.

Note that specific fish species as search terms are not needed in this query because the focus is on fisheries (fisherpeople, fishermen, fishing, fishery, fisheries), not the biology of individual fish species (unless explicitly related by the authors to fisheries). Therefore, even publications on specific fish species must use the terms fishery etc.

``` Ceylon =
TS=
(
    "overfish*"
    OR (("overharvest*" OR "overexploit*") NEAR/15 ("fish*" OR "shellfish*"))
    OR "bycatch" OR "by-catch"
    OR
      (  
        ("illegal*" OR "unreport*" OR "unregulated" OR "destructive" OR "blast" OR "dynamite"
        OR "ghost"
        OR (("gear" OR "tackle") NEAR/5 ("abandoned" OR "lost" OR "discarded"))
        )
        NEAR/10
            ("fishing" OR "fisher*" OR "trawl*"
            OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
            )
      )      
)
```  

##### Phrase 2:

Topic approach: `NEAR` is changed to `AND`

``` Ceylon =
TS=
(
  ("fishery" OR "fisheries" OR "fishing"
  OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
  OR "fish stock$"
  OR ("catch" NEAR/3 ("entitlement" OR "limit$" OR "tolerance$"))
  )
  AND
      ("manage*"
      OR "restor*"
      OR "protect*" OR "conservation"
      OR "sustainab*"
      OR "assess*"
      OR "collaps*"
      OR "maximum sustainable yield*" OR "MSY"
      OR "marine stewardship council"
      OR "regional fisheries managment organi?ation$" OR "RFMOs"
      OR "UNCLOS" OR "convention on the law of the sea"
      OR "fish stocks agreement"
      OR "code of conduct for responsible fisheries" OR "CCRF"
      OR "port state measures agreement"
      )
)
```

## Target 14.5

> **14.5 By 2020, conserve at least 10 per cent of coastal and marine areas, consistent with national and international law and based on the best available scientific information**
>
> 14.5.1 Coverage of protected areas in relation to marine areas

This query consists of 2 phrases. **All should be combined with marine terms with `AND`**

##### Phrase 1:

Again, here, the focus is on conserving marine areas. Therefore the words int he final section are included to exclude publications which may just mention marine protected areas (e.g. a place where fieldwork was carried out).

``` Ceylon =
TS=
(
  "MPA" OR "MPAs"
  OR "marine protected area$"
  OR "reserve" OR "reserves"
  OR "marine park$"
  OR "marine conservation zone$"
  OR
  (
    ("protected" OR "protection")
    NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$")
  )
  OR
  (
    ("conserved" OR "conservation" OR "conserves" OR "conserving")  
    NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$")
  )
  OR ("no-take" NEAR/3 ("area*" OR "zone*"))
  OR "conservation action$"
)
```

##### Phrase 2:

`BBNJ` is a narrow concept specifically related to difficulties conserving beyond national boundaries, so any publications mentioning it are likely to be relevant.

``` Ceylon =
TS=
(
  (
    ("biodivers*" OR "biological diversity")
    NEAR/3 ("beyond national jurisdiction" OR "beyond areas of national jurisdiction" OR "ABNJ")
  )
  OR "BBNJ"
)
```

## Target 14.6

> **14.6 By 2020, prohibit certain forms of fisheries subsidies which contribute to overcapacity and overfishing, eliminate subsidies that contribute to illegal, unreported and unregulated fishing and refrain from introducing new such subsidies, recognizing that appropriate and effective special and differential treatment for developing and least developed countries should be an integral part of the World Trade Organization fisheries subsidies negotiation***
>
><sup>*Taking into account ongoing World Trade Organization negotiations, the Doha Development Agenda and the Hong Kong ministerial mandate.</sup>
>
>  14.6.1 Degree of implementation of international instruments aiming to combat illegal, unreported and unregulated fishing

This query consists of 1 phrase.

This query finds subsidies/WTO/ODA related to fisheries (final section) which concern either a) least developed countries and small-island developing states (second section) or b) overfishing/harmful fishing (first section).

``` Ceylon =
TS =
(
  (
    ("overfish*"
    OR (("overharvest*" OR "overexploit*") NEAR/15 ("fish*" OR "shellfish*"))
    OR "bycatch" OR "by-catch"
    OR
      (  
        ("illegal*" OR "unreport*" OR "unregulated" OR "destructive" OR "blast" OR "dynamite"
        OR "ghost"
        OR (("gear" OR "tackle") NEAR/5 ("abandoned" OR "lost" OR "discarded"))
        OR "overcapacity"
        )
        NEAR/15
            ("fishing" OR "fisher*" OR "trawl*"
            OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
            )
      )  
    )
  OR
    (
      "developing world"
      OR
        (
          ("developing" OR "least developed")
          NEAR/3
              ("state*" OR "nation$" OR "countr*")
        )
      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
	    OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands"
     )
  )
  AND
      (
        ("ODA" OR "official development assistance"
        OR "world trade organisation" OR "WTO"
        OR "government* subsid*"
        OR "economic subsid*"
        OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
        OR "price support$"
        OR "tax break$"
        )
      AND
        ("fishing" OR "fisher*"
        OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
        )  
      )
)
```

## Target 14.7

> **14.7 By 2030, increase the economic benefits to small island developing States and least developed countries from the sustainable use of marine resources, including through sustainable management of fisheries, aquaculture and tourism**
>
> 14.7.1 Sustainable fisheries as a proportion of GDP in small island developing States, least developed countries and all countries

This query consists of 1 phrase. **All should be combined with marine terms with `AND`**

This query combines various economic uses and terms with sustainability. Note that this target specifically only concerns least-developed countries and SIDS, thus these are included. Here, the target is internally inconsistent with the indicator, which also concerns developing states and all countries.

``` Ceylon =
TS =
(
    (
      ("sustainab*"
      NEAR/15
          ("tourism" OR "ecotourism" OR "tourist$" OR "whale watch*" OR "sightsee*"
          OR "recreation*"
          OR "aquaculture" OR "fish farm*"
          OR "fisher*" OR "fishing" OR "harvest*"
          OR "exploit*"
          OR "use" OR "using"
          OR "manag*"
          OR "livelihood$"
          OR "social-ecological system$" OR "socialecological system$"
          OR "econom*"
          )
      )
      OR "bio-econom*" OR "bioeconom*"
      OR "blue growth" OR "blue econom*" OR "blue bond$"
      OR (("marine spatial planning" OR "ecosystem based management") AND "econom*")
    )
  AND
    (
      ("least developed"
      NEAR/3 ("state*" OR "nation$" OR "countr*" OR "small island*" OR "Pacific island*")
      )
      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
      OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands"
    )
)

```

## Target 14.a

> **14.a Increase scientific knowledge, develop research capacity and transfer marine technology, taking into account the Intergovernmental Oceanographic Commission Criteria and Guidelines on the Transfer of Marine Technology, in order to improve ocean health and to enhance the contribution of marine biodiversity to the development of developing countries, in particular small island developing States and least developed countries**
>
> 14.a.1 Proportion of total research budget allocated to research in the field of marine technology

This query consists of 3 phrases. **All should be combined with marine terms with `AND`**

##### Phrase 1:

Concerns contributions of biodiversity to the development of least developed countries and small island developing states. We include `ecosystem services` as a contribution of biodiversity to these countries.

``` Ceylon =
TS=
(
    ("blue growth" OR "blue econom*" OR "blue bond$"
    OR "bioprospect*"
    OR "biopiracy"
    OR ("bioactive" NEAR/3 ("compound*" OR "substance*"))
    OR "bioresource$" OR "biological resource$" OR "genetic resource$"
    OR "biotechnolog*"
    OR
      (
        ("biodivers*" OR "diversity")
        NEAR/15
            ("development"
            OR "livelihood$"
            OR "fisher*" OR "fishing"
            OR "harvest*"
            OR "tourism" OR "ecotourism" OR "tourist$"
            OR ("ecosystem*" NEAR/3 "service$")
            OR "Nagoya protocol"
            )
      )
    )
  AND
    (
      (("developing" OR "least developed")
      NEAR/3 ("state*" OR "nation$" OR "countr*" OR "small island*" OR "Pacific island*")
      )
      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
      OR "Antigua and Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Federated states of Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "Saint Vincent and the Grenadines" OR "Samoa" OR "São Tomé and Príncipe" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Tuvalu" OR "Vanuatu" OR "American Samoa" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "British Virgin Islands" OR "Cayman Islands" OR "Commonwealth of Northern Marianas" OR "Cook Islands" OR "Curaçao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "U.S. Virgin Islands"  
    )
)
```

##### Phrase 2:

Technology transfer simple terms.

``` Ceylon =
TS=
(
  "transfer of marine technolog*"
  OR "marine technology transfer"
)
```

##### Phrase 3:

Concerns increasing scientific knowledge, research capacity and transfer of marine technology to improve ocean health. This phrase attemts to link various kinds of scientific and knowledge infratstuctures to "ocean health" terms - a very broad concept.

The term `build*` in the first section covers capacity building.

Topic approach: `NEAR` is changed to `AND`

``` Ceylon =
TS=
(
    (
      ("share$" or "sharing"
      OR "develop*" OR "establish*" OR "increas*" OR "improv*" OR "build*" OR "implement*"
      OR "capacity development" OR "develop* capacity"  
      OR "invest" OR "investment$" OR "investing"
      OR "joint research" OR "joint effort$" OR "collaborat*" OR "international cooperation"
      )
      AND
          (
            (
              ("research" OR "scientific" OR "science")
              NEAR/5
                  ("policy" OR "policies" OR "programme$"
                  OR "advisor$"
                  OR "framework$" OR "initiative$"
                  OR "capacity" OR "capabilit*"
                  OR "infrastructure" OR "facilities" OR "vessel$" OR "vehicle$"
                  OR "network$"
                  )
            )
          OR "observ* network$" OR "observ* system$"
          OR "data infrastructure$" OR "data network$"
          OR "monitoring network$" OR "ecological monitoring"
          OR (("ocean*" OR "marine" OR "biological") NEAR/2 ("observator*" OR "monitoring"))
          OR
            (
              ("taxonom*" OR "genom*" OR "species")
              NEAR/5
                  ("knowledge" OR "research" OR "capacity" OR "compentence$"
                  OR "database$" OR "register$" OR "inventory" OR "inventories"
                  )            
            )
          )
    )
  AND
    (
       ("biodiversity" OR ("biological" NEAR/3 "diversity")
    OR (("ocean*" OR "marine") NEAR/3 ("research" OR "science"))
    OR "ocean health" OR "ecosystem health" OR "healthy ocean$"
    )
)
```

## Target 14.b

> **14.b Provide access for small-scale artisanal fishers to marine resources and markets**
>
> 14.b.1 Degree of application of a legal/regulatory/ policy/institutional framework which recognizes and protects access rights for small-scale fisheries

This query consists of 1 phrase.

Again, here, specific fish species as search terms are not needed because the focus is on fisheries (fisherpeople, fishermen, fishing, fishery, fisheries), NOT the biology of individual fish species (unless explicitly related by the authors to fisheries)

``` Ceylon =
TS =
(
    (
      ("fisher*" OR "fishing"
      OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
      )
      NEAR/5
          ("small-scale"
          OR "artisan*"
          OR "tradition*"
          OR "subsistence"
          )    
    )
  AND
    ("access*" OR "use* right$" OR "ownership" OR "control$" OR "equitab*" OR "inequitab*")    
)

```

## Target 14.c

> **14.c Enhance the conservation and sustainable use of oceans and their resources by implementing international law as reflected in the United Nations Convention on the Law of the Sea, which provides the legal framework for the conservation and sustainable use of oceans and their resources, as recalled in paragraph 158 of “The future we want”**
>
> 14.c.1 Number of countries making progress in ratifying, accepting and implementing through legal, policy and institutional frameworks, ocean-related instruments that implement international law, as reflected in the United Nations Convention on the Law of the Sea, for the conservation and sustainable use of the oceans and their resources

This query consists of 1 phrase. **It should be combined with marine terms with `AND`**

``` Ceylon =
TS =
(
    ("conserv*" OR "blue growth"
    OR
      ("sustainab*"
      NEAR/15
          ("use"
          OR "exploit*"
          OR "manag*"
          OR "govern*"
          OR "fisher*" OR "fishing" OR "harvest*"
          OR "tourism" OR "ecotourism" OR "tourist$"
          OR "aquaculture" OR "fish farm*"
          OR "resource$"
          OR "economy"
          )
      )  
    )
  AND
    ("law of the sea" OR "UNCLOS"
    OR "the future we want"
    OR (("biodivers*" OR "biological diversity") NEAR/3 ("beyond national jurisdiction" OR "ABNJ"))
    OR "BBNJ"
    OR "common fisheries policy"
    OR "deep-sea fisheries guidelines" OR "Management of Deep-sea Fisheries in the High Seas"
    OR ("convention$" NEAR/3 ("Conservation of Antarctic Living Marine Resources" OR "biological diversity" OR "OSPAR"))
    OR ("directive$" NEAR/3 ("marine strategy framework" OR "water framework" OR "marine spatial planning"))
    OR "MSFD"
    OR ("international" NEAR/3 ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*"))
    )
)

```

## General SDG

Structured slightly differently to the other goals as "water" is too general a word to use (also central to SDG 6).

``` Ceylon =
TS =
(
  "SDG14" OR "SDG 14" OR "SDG-14" OR "sustainable development goal$ 14"
  OR (("sustainable development goal$" OR "SDG$" OR "goal 14") AND "life below water")
  OR (("sustainable development goal$" OR "SDG$" OR "goal 14") NEAR/15 "oceans")
)

```

## Footnotes

<b id="f1">1</b> This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)".
(https://unstats.un.org/sdgs/indicators/indicators-list/) [↩](#SDGT+Is)

<b id="f2">2</b> United Nations (2019) World Economic Situation and Prospects (Statistical Annex). https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)
