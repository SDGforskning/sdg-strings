# Search query for SDG 14 - Life below water, Bergen action-approach.

**Contents**

1. Full query in copy-pasteable format
2. General notes about method for SDG 14
3. Marine terms: String for limiting certain phrases to the marine environment
4. Documentation and string sections for each target
5. Authorship and review
6. Footnotes


## 1. Full query

<details>
  <summary>Click to show the final copy-pasteable full query for SDG 14</summary>

Note that this query should be run in multiple steps, and then combined as shown in the final steps.

Search #1
```

```
Search #2
```

```
Search #3
```

```
Search #4
```

```
Search #5
```

```
Search #6
```

```
Search #7
```

```
Search #8
```

```
Search #9
```

```
Search #10
```

```
Search #11
```

```
Search #12
```

```
Search #13
```

```
Search #14
```

```
Search #15
```

```

</details>

## 2. General notes

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Lists of least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) are from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) - countries were included if they appeared in the tables from 2016 to 2021 (i.e. were on these lists at any time between Nov 2015 and Dec 2020) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f2)</a>).

This SDG is interpreted to be about the marine environment; however, certain topics are difficult to limit to only this environment without missing large numbers of works. In particular, fisheries research may not always use clear marine words, or may concern both marine and freshwater environments. Thus, the fishery-related targets are currently not limited using the *marine terms* below.

## 3. Marine terms: String for limiting certain phrases to the marine environment

This query is referred to as **marine terms**, and should be combined with various other sets with `AND` (when instructed) to limit the results to the marine environment. It is not combined with fishery targets.

The first part (`TS=`) consists of marine habitats, physical features, and terms to do with the coast. The second part (`SO=`) consists of marine journal titles. Journal name is used as not all publications use marine words in their abstract, title or keywords (e.g. if they are discussing a specifc marine species for an audience who knows it is marine). Journals were not included if they had non-marine elements in the title (e.g. Freshwater or Atmospheric). List gathered from Master journal list in Web of Science. The first line of this segment will find journals that begin with `"marine*" OR "ocean*" OR "estuar*" OR "deep sea*"`.

`seaweed$` and `macroalga*` are combined with other terms to prevent inclusion based on mentions of seaweeds (e.g. seaweed extracts used in industrial processes). `coast` and `sea` are combined with other terms to avoid results that are not really about the ocean (e.g. terrestrial work in "Mediterranean Sea countries"). `harbour` is  combined due to its use as a verb, and `port` due to use in other fields (e.g. electronics).

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
  OR "salt marsh*" OR "mud flat$" OR "mudflat$" OR "*tidal flat" OR "*tidal flats"
  OR "estuar*" OR "fjord$"
  OR "sea ice"

  OR "mangrove$"
  OR "kelp bed$" OR "kelp forest$"
  OR (("seaweed$" OR "macroalga*") NEAR/5 ("bed$" OR "assemblage$" OR "communit*"))
  OR "seagrass*"
  OR "sponge ground$" OR "organic fall$"
  OR "reef" OR "reefs"

  OR "coastal habitat$" OR "coastal ecosystem$" OR "coastal dune$" OR "coastal wetland$"
  OR "coastal water$"
  OR "coastal communit*" OR "coastal zone management"
  OR (
      ("coast*" OR "*tidal")
      NEAR/15
          ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$"
          OR "offshore" OR "current$"
          OR "fish*" OR "aquaculture" OR "shrimp" OR "shellfish"
          )
     )
     OR (
         ("sea")
         NEAR/15
             ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$"
             OR "offshore" OR "ship*"
             OR "fish*" OR "aquaculture" OR "shrimp" OR "shellfish"
             OR "*tidal" OR "pelagic"
             )
        )
      OR (
          ("harbour$" OR "port" OR "ports")
          NEAR/15
              ("sea" OR "coast*" OR "gulf" OR "ship*" OR "maritime")
         )
)

OR

SO =
(
  "marine*" OR "ocean*" OR "estuar*" OR "deep sea*"
  OR "Annual review of marine*"
  OR "Advances in marine*"
  OR "African journal of marine*"
  OR "Applied ocean*"
  OR "Acta ocean*"
  OR "Annales de l institut ocean*"
  OR "Archive of fishery and marine*"
  OR "Asia-pacific journal of ocean law and policy"
  OR "Biologiya moray marine*"
  OR "Bulletin of marine*"
  OR "Brazilian journal of ocean*"
  OR "California cooperative ocean*"
  OR "Cahiers de biologie marine*"
  OR "Cahiers orstom ocean*"
  OR "China ocean*"
  OR "Ciencias Marinas"
  OR "Coastal engineering"
  OR "Coral reefs"
  OR "Esturaries and coasts"
  OR "Estuarine coastal and shelf science"
  OR "Frontiers in marine*"
  OR "Fisheries ocean*"
  OR "Fishery bulletin of the national ocean*"
  OR "IEEE journal of ocean*"
  OR "International journal of naval architecture and ocean*"
  OR "Geo marine*"
  OR "Gulf and Caribbean Research"
  OR "Helgoland marine*"
  OR "ICES journal of marine*"
  OR "Indian journal of marine*"
  OR "International journal of marine*"
  OR "Journal of experimental marine*"
  OR "Journal of geophysical research ocean*"
  OR "Journal of marine*"
  OR "Journal of the marine*"
  OR "Journal of ocean*"
  OR "Journal of operational ocean*"
  OR "Journal of physical ocean*"
  OR "Journal of sea research"
  OR "Journal of the waterway port coastal and ocean*"
  OR "Mediterranean marine science"
  OR "Meeresforschung reports on marine*"
  OR "mer marine*"
  OR "molecular marine*"
  OR "New Zealand journal of marine*"
  OR "Physical ocean*"
  OR "Progress in ocean*"
  OR "PROCEEDINGS OF THE INSTITUTION OF CIVIL ENGINEERS-MARITIME ENGINEERING"
  OR "Regional studies in marine*"
  OR "Research in marine*"
  OR "Revista de biologia marina y ocean*"
  OR "Russian journal of marine*"
  OR "Scientia marina"
  OR "Sea technology"
  OR "Ships and offshore structures"
  OR "South African journal of marine*"
  OR "Thalassas"
  OR "Transnav international journal on marine*"
  OR "Vie et milieu serie a biologie marine*"
  OR "Vie et milieu serie b ocean*"
)

```
## 4. Targets

## Target 14.1

> **14.1 By 2025, prevent and significantly reduce marine pollution of all kinds, in particular from land-based activities, including marine debris and nutrient pollution**
>
> 14.1.1 (a) Index of coastal eutrophication; and (b) plastic debris density

This target is interpreted to cover research about the prevention and reduction of marine pollution (all kinds). We consider the establishment/imrpovement of pollution monitoring to fall under prevention.

**All phrases should be combined with marine terms with `AND`**. This query consists of 3 phrases, the basic structure is *action + pollution*. The pollution terms are mostly the same between them; the difference is how closely they are combined with the various action terms (closely combined terms in phrase 1 (`NEAR/5`), medium in phrase 2 (`NEAR/15`), and loosely in phrase 3 (`AND`)).

<a id="Marinepoll">[Lloyd-Smith and Immig (2018)](#f3)</a> was used to supplement with marine pollution types, as well as types mentioned in relation to the Global Programme of Action for the Protection of the Marine Environment from Land-based Activities <a id="marinepollUN">[UN Environment Programme, n.d.](#f4)</a>. The `NOT PM.2.5 OR PM10` expression at the end was included to remove aspects of atmospheric pollution which can include terms for coast.

#### Phrase 1

`tackle` is not included as an action term as it could be a type of marine debris.

`pollution` covers various kinds (e.g. noise pollution). `"effluent$" OR "runoff" OR "run off" OR "eutrophicat*" OR "ecotox*" OR "pesticide$"` will cover various types of pollution from agriculture and aquaculture. `waste OR discharge` are limited to certain fields as they are such general words (e.g. fish waste, heat waste). In this phrase, some pollutants (e.g. `mercury`) need to be combined with `pollution or contamination`, because there are papers discussing their removal from e.g. gases in industrial processes using marine organisms.

```Ceylon =
TS=
(
  (
    ("prevent*" OR "avoid*" OR "stop*" OR "remov*" OR "eliminat*" OR "combat" OR "fight"
    OR "minimi*" OR "restrict*" OR "mitigat*" OR "alleviat*" OR "reduc*" OR "decreas*"
    OR "prohibit*"
    OR "remediate" OR "remediation" OR "cleanup" OR "clean up"
    )  
    NEAR/5
        (  "pollut*"
        OR "wastewater" OR "waste water" OR "sewage"
        OR "eutrophicat*" OR "excess nutrient$" OR "excessive nutrients"
        OR "effluent$" OR "runoff" OR "run off"
        OR
          (
            ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "radioactive")
            NEAR/15
                ("waste" OR "discharge")          
          )
        OR "waste management"
        OR "litter" OR "littering" OR "garbage patch"
        OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
        OR "plastic$" OR "microplastic$" OR "micro plastic$"
        OR
          (
            ("heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT" OR "mercury" OR "mining" OR "mine tailing$" OR "oil")
            NEAR/15
                ("contamination" OR "pollut*")          
          )
        OR "contaminated" OR "contaminant$" OR "bioaccumula*" OR "ecotox*"
        OR "endocrine disrupting chemical$"
        OR "persistent organic pollutant$" OR "pesticide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
        OR "polycyclic aromatic hydrocarbon$"
        OR "oil spill$"
        )
  )
  NOT ("PM2.5" OR "PM10")
)

```

#### Phrase 2

The development of `indicators` is included as part of prevention (monitoring).

`pollution` covers various kinds (e.g. noise pollution). `"effluent$" OR "runoff" OR "run off" OR "eutrophicat*" OR "ecotox*" OR "pesticide$"` will cover various types of pollution from agriculture and aquaculture. `waste OR discharge` are limited to certain fields as they are such general words (e.g. fish waste, heat waste).

```Ceylon =
TS=
(
  (
    (
        ("treatment" OR "recovery"
        OR "technolog*"
        OR "monitor*" OR "assess*"
        OR "indicator$" OR "bioindicator$" OR "index" OR "indices"
        OR "life cycle assess*"
        OR "environment* assess*" OR "environment* impact assess*"
        OR "manag*" OR "pollution control$"
        OR "strategy" OR "strategies" OR "regulat*" OR "legislat*" OR "policy" OR "policies" OR "framework" OR "programme"
        )
        NEAR/5
            ("improv*" OR "strengthen*" OR "enhanc*" OR "scal* up" OR "upgrad*"
            OR "develop" OR "developing" OR "implement*" OR "establish*" OR "build*" OR "propose*" OR "introduce" OR "design*" OR "adopt*"
            OR "enforc*" OR "prioriti*"
            )
    )  
    NEAR/15
        (  "pollut*"
        OR "wastewater" OR "waste water" OR "sewage"
        OR "eutrophicat*" OR "excess nutrient$" OR "excessive nutrients"
        OR "effluent$" OR "runoff" OR "run off"
        OR
          (
            ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "radioactive")
            NEAR/15
                ("waste" OR "discharge")          
          )
        OR "waste management"
        OR "litter" OR "littering" OR "garbage patch"
        OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
        OR "plastic$" OR "microplastic$" OR "micro plastic$"
        OR
          (
            ("heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT" OR "mercury" OR "mining" OR "mine tailing$" OR "oil")
            NEAR/15
                ("contamination" OR "pollut*")          
          )
        OR "contaminated" OR "contaminant$" OR "bioaccumula*" OR "ecotox*"
        OR "endocrine disrupting chemical$"
        OR "persistent organic pollutant$" OR "pesticide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
        OR "polycyclic aromatic hydrocarbon$"
        OR "oil spill$"
        )
  )
  NOT ("PM2.5" OR "PM10")
)

```

#### Phrase 3

`limit pollution` was specified to avoid "pollution limits". The OSPAR convention is the Convention for the protection of the marine environment of the North-East Atlantic, and covers the prevention and elimination of pollution. The Water Framework Directive and Marine Strategy Framework Directives from the EU, and covers pollution and marine litter (respectively) as one of their topics. Global Programme of Action for the Protection of the Marine Environment from Land-based Activities is hosted by the UN environment program, and is an intergovernmental action program.

`pollution` covers various kinds (e.g. noise pollution). `"effluent$" OR "runoff" OR "run off" OR "eutrophicat*" OR "ecotox*" OR "pesticide$"` will cover various types of pollution from agriculture and aquaculture. In this phrase, specific pollutants (e.g. `mercury`) do not need to be combined with `pollution or contamination`, because the action terms are all related to pollution.

```Ceylon =
TS=
(
  (
    ("limit pollut*" OR "control pollut*"
    OR "biosorption" OR "bioremediat*"
    OR "water framework directive" OR "OSPAR convention" OR "Marine strategy framework directive"
    OR "Global Programme of Action for the Protection of the Marine Environment"
    )
    AND
        (  "pollut*"
        OR "wastewater" OR "waste water" OR "sewage"
        OR "eutrophicat*" OR "excess nutrient$" OR "excessive nutrients"
        OR "effluent$" OR "runoff" OR "run off"
        OR
          (
            ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "radioactive")
            NEAR/15
                ("waste" OR "discharge")          
          )
        OR "pesticide$"
        OR "waste management"
        OR "litter" OR "littering" OR "garbage patch"
        OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
        OR "plastic$" OR "microplastic$" OR "micro plastic$"
        OR "heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT" OR "mercury"
        OR "mining" OR "mine tailing$"
        OR "oil"
        OR "contaminated" OR "contaminant$" OR "bioaccumula*" OR "ecotox*"
        OR "endocrine disrupting chemical$"
        OR "persistent organic pollutant$" OR "pesticide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "Pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
        OR "polycyclic aromatic hydrocarbon$"
        )
  )
  NOT ("PM2.5" OR "PM10")
)

```

## Target 14.2 & 14.5

> **14.2 By 2020, sustainably manage and protect marine and coastal ecosystems to avoid significant adverse impacts, including by strengthening their resilience, and take action for their restoration in order to achieve healthy and productive oceans**
>
> 14.2.1 Number of countries using ecosystem-based approaches to managing marine areas

> **14.5 By 2020, conserve at least 10 per cent of coastal and marine areas, consistent with national and international law and based on the best available scientific information**
>
> 14.5.1 Coverage of protected areas in relation to marine areas

Target 14.2 is interpreted to cover research about a) management of marine ecosystems, b) protection of these ecosystems, and c) restoring these ecosystems. It also talks about management/protection to avoid "adverse impacts", implying that research about the impacts of protected/managed areas is relevant. 14.5 is interpreted to cover research about the establishment and management of marine protected areas.

While 14.2 is not explicitly about establishing marine protected areas (as we see in target 14.5), "protect" is still used as one of the actions, suggesting that research on the establishment of MPAs falls under 14.2 too (amongst research on other aspects of protection, such as the impacts of other protection measures). A string for 14.5 is still retained, but the research found there will also be covered under 14.2. 14.5 is just a more specific area.

**All phrases should be combined with marine terms with `AND`**

This query consists of 3 phrases.

##### Phrase 1:

This phrase covers terms for sustainable management, protection, and restoration. These terms are included without action terms, as management/restoration are actions themselves. This means the phrase will also find research about the impacts of these actions.

Various types of management framework and protected areas are included, as well as some specific pieces of legislation (e.g. Conservation of Antarctic Marine Living Resources).

`BBNJ` is a narrow concept most often used to highlight the difficulties conserving biodiversity beyond national waters, so any publications mentioning it are likely to be about protection/management.

```Ceylon =
TS=
(
  "marine spatial planning" OR "spatial management"
  OR "coastal zone management" OR "integrated coastal zone planning"
  OR "locally managed marine area$" OR "LMMA$"
  OR
    (
      ("ecosystem-based" OR "area-based")
      NEAR/5 ("manag*" OR "approach*" OR "govern*")
    )
  OR  
    ("sustainab*"
    NEAR/5 ("manag*" OR "govern*")
    )
  OR "MPA" OR "MPAs" OR "marine protected area$"
  OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
  OR "marine conservation zone$"
  OR "particularly sensitive sea areas$"
  OR
    (
      ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving")
      NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$")
    )
  OR "Conservation of Antarctic Marine Living Resources"  
  OR "International coral reef initiative"
  OR
    (
      ("biodivers*" OR "biological diversity")
      NEAR/3 ("beyond national jurisdiction" OR "beyond areas of national jurisdiction" OR "ABNJ")
    )
  OR "BBNJ"
  OR
    ("no-take"
    NEAR/3 ("area*" OR "zone*")
    )
  OR  
    (
      ("restore" OR "restored" OR "restoration")
      NEAR/5 ("ecosystem$" OR "habitat$")
    )
)
```

##### Phrase 2:

This phase is about sustainable management, protection and restoration, connected to the positive impacts mentioned in the target (health & ecosystem resilience, and production). It aims to find works talking about impacts, or drivers of the impacts, in managed/protected/restored areas. The basic structure is *management/protection/restoration + action + ocean health/productivity*.

The *ocean health* terms include various terms to do with functioning ecosystems. "ecosystem functioning" and "ecosystem services" are terms used in biology about the biological functioning of the ecosystem and services it provides to humans, respectively. `diversity` elements are included as diversity at various levels is important for ecosystem functioning, resilience and services (though not necessarily linearly). `key species` and `foundation species` are species whose presence is important for ecosystem maintenance/creation. `water quality` is included as this can be a driver of key species loss.

The *productivity* terms include terms suggested by the phrase "productive oceans"; it is interpreted as referring to products for humans, rather than e.g. primary production. Fish stocks are not the only important product from the ocean. Should more be included here?

```Ceylon =
TS=
(
  ("manag*" OR "protect*" OR "conserv*" OR "restore" OR "restoration")
  NEAR/15
    (
      ("increas*" OR "strengthen" OR "improv*" OR "enhance" OR "facilitat*"
      OR "preserv*" OR "support*" OR "ensure" OR "sustain"
      )
      NEAR/3
          ( ("ocean$" NEAR/3 "health$")
          OR
            (
              ("ecosystem$" OR "habitat$" OR "environment*")
              NEAR/3 ("health$" OR "recovery" OR "service$" OR "functioning" OR "function$" OR "quality")
            )
          OR "resilien*"
          OR "water quality"
          OR "biodiversity" OR "species diversity" OR "functional diversity" OR "genetic diversity"
          OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species"
          OR "productivity" OR "food production" OR "fish stock$"
          )
    )
)
```

##### Phrase 3:

This phrase is the opposite of phrase 2 - it covers negative impacts on ocean health and productivity.

```Ceylon =
TS=
(
  ("manag*" OR "protect*" OR "conserv*" OR "restore" OR "restoration")
  NEAR/15
    (
      ("avoid" OR "prevent*" OR "decreas*" OR "reduc*" OR "stop" OR "limit" OR "minimi*" OR "mitigat*")
      NEAR/3
          (
            (("ecosystem$" OR "habitat$") NEAR/3 ("decline$" OR "collapse" OR "dead zone$" OR "degradation" OR "loss"))
            OR ("biodiversity" NEAR/3 "loss*")
            OR (("fisheries" OR "fishery" OR "fish stock$") NEAR/3 ("decline$" OR "collapse"))
          )    
    )
)
```

## Target 14.5

> **14.5 By 2020, conserve at least 10 per cent of coastal and marine areas, consistent with national and international law and based on the best available scientific information**
>
> 14.5.1 Coverage of protected areas in relation to marine areas

The target is interpreted to cover research about the establishment and management of marine protected areas. **See notes on 14.2** (*While 14.2 is not explicitly about  marine protected areas (as we see in target 14.5), "protect" is still used as one of the actions, suggesting that research on the establishment/maintenance of MPAs falls under 14.2 too (amongst research on other aspects of protection, such as the impacts of other measures). A string for 14.5 is still retained, but the research found there will also be covered under 14.2. 14.5 is just a more specific area.*)

This query consists of 1 phrase. **It should be combined with marine terms with `AND`**

Conserving areas of the ocean is considered widely to include several types of protected areas (which have different degress of protection); for exmaple, `no take zone$`, `conservation zone$`, `marine protected area$`.

``` Ceylon =
TS=
(
  ("MPA" OR "MPAs" OR "marine protected area$"
  OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
  OR "marine conservation zone$"
  OR "particularly sensitive sea areas$"
  OR
    (
      ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving")
      NEAR/3 ("area*" OR "zone*" OR "habitat$" OR "ecosystem$")
    )
  OR
    ("no-take"
    NEAR/3 ("area*" OR "zone*")
    )
  )
  NEAR/15
      ("designat*" OR "placement" OR "delineat*"
      OR "design" OR "create" OR "creation"
      OR "establish*" OR "propose*" OR "proposal$" OR "implement*"
      OR "plans" OR "plan" OR "planned" OR "planning"
      OR "priorit*"
      OR "manage*" OR "enforce" OR "enforcement"
      )
)
```

## Target 14.3

> **14.3 Minimize and address the impacts of ocean acidification, including through enhanced scientific cooperation at all levels**
>
> 14.3.1 Average marine acidity (pH) measured at agreed suite of representative sampling stations

This query consists of 1 phrase. **It should be combined with marine terms with `AND`**

The target is interpreted to cover research that focuses on the impacts of acidification, so that these can be minimized and addressed. "Minimize [the impacts]" is ok to interpret, but "address the impacts" is harder to know what it covers. Thus this query is left open in terms of actions. The basic structure is *acidification + impacts*.

`ph` was considered as an *acidification* term, but returns results from industrial processes, thus is combined in phrases. `OA` will find "okadeic acid" (shellfish poisoning) if used alone, hence the `AND ocean$` term (marine is not included, as often use "marine toxin").

`calcification` and related terms are included here as *impacts*, as this biological process is one of the big concerns in terms of impacts of acidification. Also included are effect terms generally (e.g. `impact*`) and major biological processes that can be impacted (e.g. `reproduction`).

``` Ceylon =
TS =
(
  (
    ("acidif*" OR "OA"
    OR "ocean ph" OR "low ph" OR "declining ph" OR "decreas* ph" OR "effect$ of ph" OR "effect$ of seawater ph"
    )
    NEAR/15
        ("impact*" OR "effect$" OR "affect$" OR "response$" OR "consequence$" OR "results in" OR "changes" OR "alter*"
        OR "sensitiv*" OR "vulnerab*" OR "threat"
        OR "calcif*" OR "decalcif*" OR "calcium carbonate" OR "dissol*" OR "aragonite" OR "calcite" OR "carbonate saturation"
        OR "extinction" OR "adaptation" OR "adaptive capacity" OR "competition" OR "recruitment" OR "survival" OR "reproduction"
        )
  )
  AND "ocean$"
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
  ( "prevent*" OR "avoid*" OR "stop*" OR "prohibit*"
  OR "tackling" OR "tackle" OR "restrict*"
  OR "reduc*" OR "decreas*" OR "minimi*" OR "mitigat*" OR "remov*" OR "limit$" OR "limiting" OR "limited"
  OR "manag*" OR "regulat*" OR "law$" OR "strateg*" OR "policy" OR "policies"
  OR "marine stewardship council"
  OR "regional fisheries management organi?ation$" OR "RFMOs"
  OR "UNCLOS" OR "convention on the law of the sea"
  OR "fish stocks agreement"
  OR "code of conduct for responsible fisheries" OR "CCRF"
  OR "port state measures agreement"
  )
  NEAR/10
      ("overfish*"
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

``` Ceylon =
TS=
(
  ("fishery" OR "fisheries" OR "fishing"
  OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
  OR "fish stock$"
  OR ("catch" NEAR/3 ("entitlement" OR "limit$" OR "tolerance$"))
  )
  NEAR/15
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
      (("developing" OR "least developed") NEAR/3 ("state*" OR "nation$" OR "countr*"))
	   OR "developing world"
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

The term `build*` int he first section covers capacity building.

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
      NEAR/15
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
    (
      ("access*" OR "use* right$" OR "ownership" OR "control$" OR "equitab*" OR "inequitab*")
      NEAR/15
          ("market$"
          OR "trade*"
          OR "territor*"
          OR "right$"
          OR "livelihood$"
          OR "policy" OR "policies"
          OR "law$"
          OR "law of the sea"
          OR "regulat*"
          OR "institutional framework$"
          )      
    )
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

## 5. Authorship and review

## 6. Footnotes

<a id="f3"></a> Lloyd-Smith and Immig. (2018). *Ocean Pollutants Guide: Toxic Threats to Human Health and Marine Life*. International Pollutants Elimination Network/National Toxics Network.  https://ipen.org/sites/default/files/documents/ipen-ocean-pollutants-v2_1-en-web.pdf. [↩](#Marinepoll)

<a id="f1"></a> Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f2"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f4"></a> UN Environment Programme. (n.d.). *Addressing Land-Based Pollution*. United Nations. https://www.unep.org/explore-topics/oceans-seas/what-we-do/addressing-land-based-pollution [Accessed 22 November 2021]. [↩](#marinepollUN)
