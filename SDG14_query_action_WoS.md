# Search query for SDG 14 - Life below water, Bergen action-approach.

Conserve and sustainably use the oceans, seas and marine resources for sustainable development.

**Current status**: This string is undergoing edits after internal review. It is substantially changed from the original version it was based on (v2019.11).*

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

This SDG is interpreted to be about the marine environment; however, certain topics are difficult to limit to only this environment without missing large numbers of works. In particular, fisheries research may not always use clear marine words, or may concern both marine and freshwater environments. Thus, the fishery-related targets (14.4, 14.6 and 14.b) are currently not limited using the *marine terms* below. All other areas are.

A source of keywords for several targets was OECDs "Marine Protected Areas: Economics, Management and Effective Policy Mixes" (<a id="OECD">[OECD, 2017](#f5)</a>), and FAOs "State of World Fisheries and Aquaculture" (<a id="FAOfish">[FAO, 2018](#f8)</a>). In addition, during editing of this string (2021), we have consulted two other sets of queries for reference: <a id="Aurora">[Aurora Universities network (2020)](#f5)</a> and <a id="Els">[Rivest et al. (2021)](#f6)</a>.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[Statistics Division, 2021a](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f2)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

## 3. Marine terms: String for limiting certain phrases to the marine environment

This string is referred to as **marine terms**, and should be combined with various other sets with `AND` (when instructed) to limit the results to the marine environment. It is not combined with fishery targets (14.4, 14.6 and 14.b). It does not work perfectly, as a number of publications may be about e.g. freshwater habitats, but still mention marine habitats in a comparative way. This is difficult to avoid.

The first part (`TS=`) consists of marine habitats, physical features, and terms to do with the coast. The second part (`SO=`) consists of marine journal titles. Journal search is used as not all publications use marine words in their abstract, title or keywords (e.g. if they are discussing a specifc marine species for an audience who knows it is marine). Journals were not included if they had non-marine elements in the title (e.g. Freshwater or Atmospheric). List gathered from Master journal list in Web of Science. The first line of this segment will find journals that begin with `"marine*" OR "ocean*" OR "estuar*" OR "deep sea*"`.

`seaweed$` and `macroalga*` are combined with other terms to prevent inclusion based on mentions of seaweeds (e.g. seaweed extracts used in industrial processes). `reef` is used rather than `coral` as additions only due to the latter are mostly non-relevant ("coral-like structures".) `coast` and `sea` are combined with other terms to avoid results that are not really about the ocean (e.g. terrestrial work in "Mediterranean Sea countries"). `harbour` is  combined due to its use as a verb, and `port` due to use in other fields (e.g. electronics).

I considered adding the 25 most common marine fisheries species (<a id="FAOfish">[FAO, 2018](#f8)</a>), however this gave few extra relevant results. It introduced a lot more noise with the use of `MPA` in 14.2/14.5, as this is commonly used as a unit of pressure (MPa) when discussing the processing of these species for food. Relevant species include: `"theragra chalcogramma" OR "engraulis ringens" OR "katsuwonus pelamis" OR "sardinella" OR "trachurus" OR "clupea harengus" OR "scomber japonicus" OR "thunnus albacares" OR "gadus morhua" OR "engraulis japonicus" OR "decapterus" OR "sardina pilchardus" OR "trichiurus lepturus" OR "micromesistius poutassou" OR "scomber scombrus" OR "scomberomorus" OR "dosidicus gigas" OR "nemipterus" OR "brevoortia patronus" OR "sprattus sprattus" OR "portunus trituberculatus" OR "acetes japonicus" OR "sardinops melaonstictus" OR "scomber colias" OR "rastrelliger kanagurta"`.

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

This target is interpreted to cover research about the prevention and reduction of marine pollution We consider the establishment/improvement of pollution monitoring to fall under prevention.

<a id="Marinepoll">[Lloyd-Smith and Immig (2018)](#f3)</a> was used to supplement with marine pollution types, as well as types mentioned in relation to the Global Programme of Action for the Protection of the Marine Environment from Land-based Activities <a id="marinepollUN">[UN Environment Programme, n.d.](#f4)</a>. The `NOT PM.2.5 OR PM10` expression at the end was included to remove aspects of atmospheric pollution which can include terms for coast.

It consists of 3 phrases.

#### Phrase 1

The general structure is *action + pollution*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

The pollution terms and structure are mostly the same between the three phrases; the difference is the action terms, and how closely they are combined with these (closely combined terms in phrase 1 (`NEAR/5`), medium in phrase 2 (`NEAR/15`), and loosely in phrase 3 (`AND`)). In this phrase, the action terms consist of general actions.

Action terms: `tackle` is not included as an action term as it could be a type of marine debris.

Pollution terms: `pollution` covers various kinds (e.g. noise pollution). `waste OR discharge` are limited to certain fields as they are such general words (e.g. fish waste, heat waste). In this phrase, some pollutants (e.g. `mercury`) need to be combined with `contamination`, because there are papers discussing their removal from e.g. gases in industrial processes using marine organisms. This phrase does not include `waste management` like the others because it does not fit with these action terms.

```Ceylon =
TS=
(
  (
    ("prevent*" OR "avoid*" OR "stop*" OR "remov*" OR "eliminat*" OR "combat" OR "fight"
    OR "minimi*" OR "restrict*" OR "mitigat*" OR "alleviat*" OR "reduc*" OR "decreas*"
    OR "prohibit*" OR "protect*"
    OR "remediate" OR "remediation" OR "cleanup" OR "clean up"
    )  
    NEAR/5
        (  "pollut*"
        OR "wastewater" OR "waste water" OR "sewage" OR "sewer$"
        OR "eutrophicat*" OR "excess nutrient$" OR "excessive nutrient$"
        OR "effluent$" OR "nutrient runoff" OR "nutrient run off"
        OR
          (
            ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "household$" OR "domestic" OR "urban" OR "radioactive")
            NEAR/15
                ("waste" OR "discharge" OR "runoff" OR "run off")          
          )
        OR "litter" OR "littering" OR "garbage patch"
        OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
        OR "plastic$" OR "microplastic$" OR "micro plastic$" OR "nanoplastic$" OR "nano plastic$"
        OR
          (
            ("heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT" OR "mercury" OR "toxic metal$" OR "mining" OR "mine tailing$" OR "oil")
            NEAR/15 "contamination"         
          )
        OR "contaminated" OR "contaminant$" OR "bioaccumula*" OR "ecotox*" OR "toxic chemical$"
        OR "endocrine disrupting chemical$"
        OR "persistent organic pollutant$" OR "pesticide$" OR "herbicide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
        OR "polycyclic aromatic hydrocarbon$" OR "PAH"
        OR "oil spill$"
        )
  )
  NOT ("PM2.5" OR "PM10" OR "leaf litter")
)

```

#### Phrase 2

The general structure is *action + pollution tech/treatments + pollution*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

The pollution terms and structure are mostly the same between the three phrases; the difference is the action terms, and how closely they are combined with these (closely combined terms in phrase 1 (`NEAR/5`), medium in phrase 2 (`NEAR/15`), and loosely in phrase 3 (`AND`)). In this phrase, the action terms consist of general actions and "pollution actions".

The development of `indicators` is included as part of prevention (monitoring). `pollution` covers various kinds (e.g. noise pollution). `waste OR discharge` are limited to certain fields as they are such general words (e.g. fish waste, heat waste).

```Ceylon =
TS=
(
  (
    (
        ("improv*" OR "strengthen*" OR "enhanc*" OR "scal* up" OR "upgrad*"
        OR "develop" OR "developing" OR "implement*" OR "establish*" OR "build*" OR "propose*" OR "introduce" OR "design*" OR "adopt*"
        OR "enforc*" OR "prioriti*"
        )
        NEAR/5
            ("treatment" OR "recovery"
            OR "technolog*"
            OR "monitor*" OR "assess*"
            OR "indicator$" OR "bioindicator$" OR "index" OR "indices"
            OR "life cycle assess*" OR "LCA"
            OR "environment* assess*" OR "environment* impact assess*"
            OR "manag*" OR "pollution control$"
            OR "strategy" OR "strategies" OR "regulat*" OR "legislat*" OR "policy" OR "policies" OR "framework" OR "programme"
            )
    )  
    NEAR/15
        (  "pollut*"
        OR "wastewater" OR "waste water" OR "sewage"
        OR "eutrophicat*" OR "excess nutrient$" OR "excessive nutrient$"
        OR "effluent$" OR "nutrient runoff" OR "nutrient run off"
        OR
          (
            ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "household$" OR "domestic" OR "urban" OR "radioactive")
            NEAR/15
                ("waste" OR "discharge" OR "runoff" OR "run off")          
          )
        OR "waste management"
        OR "litter" OR "littering" OR "garbage patch"
        OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
        OR "plastic$" OR "microplastic$" OR "micro plastic$" OR "nanoplastic$" OR "nano plastic$"
        OR
          (
            ("heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT" OR "mercury" OR "toxic metal$" OR "mining" OR "mine tailing$" OR "oil")
            NEAR/15 "contamination"          
          )
        OR "contaminated" OR "contaminant$" OR "bioaccumula*" OR "ecotox*" OR "toxic chemical$"
        OR "endocrine disrupting chemical$"
        OR "persistent organic pollutant$" OR "pesticide$" OR "herbicide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
        OR "polycyclic aromatic hydrocarbon$" OR "PAH"
        OR "oil spill$"
        )
  )
  NOT ("PM2.5" OR "PM10")
)

```

#### Phrase 3

The general structure is *action + pollution*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

The pollution terms and structure are mostly the same between the three phrases; the difference is the action terms, and how closely they are combined with these (closely combined terms in phrase 1 (`NEAR/5`), medium in phrase 2 (`NEAR/15`), and loosely in phrase 3 (`AND`)). In this phrase, the action terms consist of frameworks and specific phrases.

`limit pollution` was specified to avoid "pollution limits".
* The OSPAR convention is the Convention for the protection of the marine environment of the North-East Atlantic, and covers the prevention and elimination of pollution.
* The Water Framework Directive and Marine Strategy Framework Directives from the EU, and covers pollution and marine litter (respectively) as one of their topics. The Barcelona convention refers to the Mediterranean.
* Global Programme of Action for the Protection of the Marine Environment from Land-based Activities is hosted by the UN environment program, and is an intergovernmental action program.
* MARPOL is the International convention for the prevention of pollution from ships (International Maritime Organization)

`pollution` covers various kinds (e.g. noise pollution). In this phrase, specific pollutants (e.g. `mercury`) do not need to be combined with `pollution or contamination`, because the action terms are all related to pollution.

```Ceylon =
TS=
(
  (
    ("limit pollut*" OR "control pollut*"
    OR "biosorption" OR "bioremediat*"
    OR "water framework directive"
    OR "OSPAR convention"
    OR "Marine strategy framework directive"
    OR "Barcelona convention"
    OR "Global Programme of Action for the Protection of the Marine Environment"
    OR "MARPOL" OR "prevention of pollution from ships"
    )
    AND
        (  "pollut*"
        OR "wastewater" OR "waste water" OR "sewage" OR "sewer$"
        OR "eutrophicat*" OR "excess nutrient$" OR "excessive nutrient$"
        OR "effluent$" OR "runoff" OR "run off"
        OR
          (
            ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "household$" OR "domestic" OR "urban" OR "radioactive")
            NEAR/15 ("waste" OR "discharge")          
          )
        OR "waste management"
        OR "litter" OR "littering" OR "garbage patch"
        OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
        OR "plastic$" OR "microplastic$" OR "micro plastic$" OR "nanoplastic$" OR "nano plastic$"
        OR "heavy metal$" OR "organotin$" OR "tributyltin" OR "TBT" OR "mercury" OR "toxic metal$"
        OR "mining" OR "mine tailing$"
        OR "oil"
        OR "contaminated" OR "contaminant$" OR "bioaccumula*" OR "ecotox*" OR "toxic chemical$"
        OR "endocrine disrupting chemical$"
        OR "persistent organic pollutant$" OR "pesticide$" OR "herbicide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "Pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
        OR "polycyclic aromatic hydrocarbon$" OR "PAH"
        )
  )
  NOT ("PM2.5" OR "PM10")
)

```

## Target 14.2

> **14.2 By 2020, sustainably manage and protect marine and coastal ecosystems to avoid significant adverse impacts, including by strengthening their resilience, and take action for their restoration in order to achieve healthy and productive oceans**
>
> 14.2.1 Number of countries using ecosystem-based approaches to managing marine areas

Target 14.2 is interpreted to cover research about a) sustainable management of marine/coastal ecosystems, b) protection of these ecosystems, which would include establishment and management of marine protected areas (MPAs), and c) restoring these ecosystems. Note, the interpretation of protection to include establishment of MPAs means that this target also encompasses 14.5.

This query consists of 3 phrases. Phrase 1 covers the establishment/management of protected areas. Phrase 2 covers the establishment/improvement of sustainable management approaches. Phrase 3 covers research about restoring, protecting, conserving or managing marine ecosystems.

##### Phrase 1

This phrase covers the establishment/management of protected areas. The general structure is *action + protected areas*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

Conserving areas of the ocean is considered widely to include several types of protected areas (which have different degrees of protection); for example, `no take zone$`, `conservation zone$`, `marine protected area$`. The phrase `"protect*" OR "conservation" NEAR/3 "area*" or "zone"` will cover "marine protected areas" and "marine conservation zones".

```Ceylon =
TS=
(
  ("designat*" OR "placement" OR "delineat*" OR "expand*" OR "extend"
  OR "design" OR "designing" OR "create" OR "creation" OR "creating" OR "develop" OR "development"
  OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e"
  OR "plans" OR "plan" OR "planned" OR "planning"
  OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "governance" OR "manag*"
  OR "enforce" OR "enforcement" OR "enforcing"
  OR "strengthen" OR "improv*"
  )
  NEAR/5
      ("MPA" OR "MPAs" OR "LSMPA$" OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
      OR "particularly sensitive sea area$"
      OR
        (
          ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving")
          NEAR/3 ("area$" OR "zone$" OR "habitat$" OR "ecosystem$")
        )
      OR ("no-take" NEAR/3 ("area$" OR "zone*" OR "reserve$")) OR "NTMR$"
      )
)
```

##### Phrase 2

Phrase 2 covers the establishment/improvement of sustainable management approaches.  The general structure is *action + sustainable management*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

```Ceylon =
TS=
(
  ("designat*" OR "placement" OR "delineat*" OR "expand*" OR "extend"
  OR "design" OR "designing" OR "create" OR "creation" OR "creating"
  OR "establish*" OR "propos*" OR "proposal$" OR "implement*" OR "prioriti$e"
  OR "plans" OR "plan" OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "governance"
  OR "enforce" OR "enforcement" OR "enforcing"
  OR "strengthen" OR "improv*" OR "enhance" OR "facilitat*" OR "support*"
  )
  NEAR/5
      ("marine spatial planning" OR "spatial management"
      OR "coastal zone management" OR "integrated coastal zone planning" OR "ICZM"
      OR "coastal resources management"
      OR "community based management"
      OR "locally managed marine area$" OR "LMMA$"
      OR "resilience based management"
      OR "herbivore management area$"
      OR ("sustainab*" NEAR/5 ("manag*" OR "govern*"))
      OR
        (
          ("ecosystem-based" OR "area-based")
          NEAR/5 ("manag*" OR "approach*" OR "govern*")
        )
      )
)
```

##### Phrase 3

Phrase 3 covers research about restoring, protecting, conserving or managing marine ecosystems. The general structure is *action + marine ecosystems or elements*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

The *action terms* for this string are challenging because one can talk about "how to conserve the marine environment" (relevant), but could also just mention "the study was carried out in a conservation area" (less relevant). Therefore, we have action terms that are clear verbs for manage/protect etc., but combine other forms of these words with other actions (establishing, improving etc).

Under the *marine ecosystems/elements*, we include habitats, elements of ocean health, elements of production, and some specific pieces of legislation to do with conservation/protection. Terms to do with ocean health include various terms to do with functioning ecosystems and services for humans, diversity at various levels (important for ecosystem functioning, resilience and services),  `key species` and `foundation species` (whose presence is important for ecosystem maintenance), and `water quality` (can be a driver of species loss).`BBNJ` is a concept most often used to highlight the difficulties conserving biodiversity beyond national waters, so any publications mentioning it are likely to be about protection/management.

```Ceylon =
TS=
(
  ("manage" OR "conserve" OR "protect" OR "restore"
  OR
    (
      ("designat*" OR "placement" OR "expand*" OR "extend"
      OR "design" OR "designing" OR "create" OR "creation" OR "creating"
      OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e"
      OR "plans" OR "plan" OR "planned" OR "planning" OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "strategy" OR "governance"
      OR "enforce" OR "enforcement" OR "enforcing"
      OR "increas*" OR "strengthen" OR "improv*" OR "enhance" OR "facilitat*"
      OR "preserv*" OR "support*" OR "ensur*"
      )
      NEAR/5
        ("management" OR "conservation" OR "protection" OR "restoration" OR "sustainable")
    )
  )
  NEAR/15
      ("ecosystem$" OR "habitat$" OR "communit*"
      OR "mangrove$" OR "kelp bed$" OR "kelp forest$" OR "seagrass*"
      OR (("seaweed$" OR "macroalga*") NEAR/5 ("bed$" OR "assemblage$" OR "communit*"))
      OR "sponge ground$" OR "reef" OR "reefs" OR "coral$"
      OR "salt marsh*" OR "mud flat$" OR "mudflat$" OR "*tidal flat" OR "*tidal flats"
      OR "estuar*" OR "fjord$" OR "coastal habitat$" OR "coastal ecosystem$" OR "coastal dune$" OR "coastal wetland$" OR "coastal water$"
      OR
        (
          ("ocean$" OR "environment*")
          NEAR/3
              ("health$" OR "recovery" OR "service$" OR "functioning" OR "function$"
              OR "quality" OR "integrity" OR "stability" OR "resilien*"
              )
        )
      OR "water quality"
      OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
      OR ("diversity" NEAR/3 ("beyond national jurisdiction" OR "beyond areas of national jurisdiction" OR "ABNJ"))
      OR "BBNJ"
      OR "tipping point$" OR "extinction$"
      OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species"
      OR "productivity" OR "food production" OR "fish stock$" OR "fishery" OR "fisheries" OR "aquaculture"
      OR ("no-take" NEAR/3 ("area*" OR "zone*"))
      OR "Habitats directive"
      OR "CBD" OR "HELCOM" OR "OSPAR" OR "UNEP"
      OR "Conservation of Antarctic Marine Living Resources" OR "CCAMLR"
      OR "Lima convention" OR "Nairobi convention" OR "Noumea convention" OR "Barcelona convention" OR "World heritage convention"
      OR "International coral reef initiative"
      )
)
```

## Target 14.3

> **14.3 Minimize and address the impacts of ocean acidification, including through enhanced scientific cooperation at all levels**
>
> 14.3.1 Average marine acidity (pH) measured at agreed suite of representative sampling stations

The target is interpreted to cover research that focuses on minimising the impacts of ocean acidification (OA). We interpret "address" also as a term meaning to limit/combat. We also interpret this to cover research about improving resilience to OA.

The general structure is *action + impacts + acidification*.

*Acidification* terms: `ph` returns results from industrial processes, thus is combined in phrases. `OA` is a common abbreviation (e.g. osteoarthritis) and will find "okadeic acid" (shellfish poisoning) if used alone, hence the `AND ocean$` term (marine is not included, as often use "marine toxin"). Using all the marine terms (minus "marine") vs. just using `AND ocean$` actually only adds few extra results, many not relevant; likely because "ocean acidification" is a well-established term.  

*Impact terms*: In this version, general impact terms are included as these work best with action terms (e.g. `impact*`). However, for the topic approach more impact terms should be added, e.g. major biological processes that can be impacted, such as calcification: `"calcif*" OR "decalcif*" OR "calcium carbonate" OR "dissol*" OR "aragonite" OR "calcite" OR "carbonate saturation" OR "extinction" OR "adaptation" OR "adaptive capacity" OR "competition" OR "recruitment" OR "survival" OR "reproduction"`

``` Ceylon =
TS =
(
  (
    (
      (
        ("decreas*" OR "minimi*" OR "reduc*" OR "limit" OR "mitigat*" OR "alleviat*"
        OR "fight*" OR "combat*" OR "tackl*" OR "resist*"
        OR "stop*" OR "avoid*" OR "prevent*" OR "halt*"       
        )
        NEAR/5
          ("impact*" OR "effect$" OR "affect$" OR "response$" OR "consequence$"
          OR "results in" OR "changes" OR "alter*"
          OR "sensitiv*" OR "vulnerab*" OR "threat*"
          )
      )
      OR
      (
        ("increas*" OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*"
        OR "maintain*" OR "preserv*"
        )
        NEAR/5 ("resilience" OR "adaptive capacity" OR "coping" OR "toleranc*")
      )
    )
    NEAR/15
        ("acidi*" OR "OA" OR "ocean ph" OR "seawater ph"
        OR "low ph" OR "declining ph" OR "decreas* ph" OR "effect$ of ph"
        )
  )
  AND "ocean$"
)
```   

## Target 14.4

> **14.4 By 2020, effectively regulate harvesting and end overfishing, illegal, unreported and unregulated fishing and destructive fishing practices and implement science-based management plans, in order to restore fish stocks in the shortest time feasible, at least to levels that can produce maximum sustainable yield as determined by their biological characteristics**
>
> 14.4.1 Proportion of fish stocks within biologically sustainable levels

This target is interpreted to cover research about:
* ending overfishing, illegal/unreported fishing (IUU fishing), destructive fishing  (phrase 1 & 2)
* implementation of science-based fisheries management (phrase 3)

Specific fish species as search terms are not needed in this query because the focus is on fisheries (fisherpeople, fishermen, fishing, fishery, fisheries), not the biology of individual fish species outside of fisheries. Therefore, even publications on specific fish species must use the terms fishery etc.

##### Phrase 1:

The basic structure is *generic action + overfishing/illegal/destructive fishing*. The *overfishing* terms are the same in phrase 1 and phrase 2, but the action terms differ and are added at a closer distance in phrase 1.

`bycatch` is included as a form of destructive/IUU fishing, as is `blast fishing`. We also consider abandoned gear to lie under destructive fishing - even though it is not fishing per se, it is damage to marine life caused by fishing. Fishery `collapse OR closure$` are considered relevant to overfishing; even when overfishing is not the primary cause, they are related to science-based management (also covered by this target).

``` Ceylon =
TS=
(
  ("prevent*" OR "avoid*" OR "stop*" OR "end" OR "ending"
  OR "tackling" OR "tackle" OR "restrict*" OR "combat*"
  OR "reduc*" OR "decreas*" OR "minimi*" OR "mitigat*" OR "remov*" OR "limit$" OR "limiting" OR "limited"
  OR "manag*" OR "regulat*" OR "solution$" OR "monitor*"
  )
  NEAR/5
      ("overfish*"
      OR "bycatch" OR "by-catch"
      OR "IUU fishing"
      OR (("gear" OR "nets") NEAR/5 ("abandoned" OR "lost" OR "discarded"))
      OR "ghost fishing" OR "ghost nets" OR "ALDFG"
      OR
        (
          ("overharvest*" OR "overexploit*" OR "overcapacity" OR "collaps*" OR "closure$"
          OR "illegal*" OR "unreport*" OR "unregulated" OR "corruption" OR "destructive" OR "blast" OR "dynamite" OR "cyanide"
          )
          NEAR/15 ("fishing" OR "fisher*" OR "shellfish*" OR "trawl*")
        )
      )       
)
```

##### Phrase 2:

The basic structure is *instrument actions + overfishing/illegal/destructive fishing*. The *overfishing* terms are the same in phrase 1 and phrase 2, but the action terms differ and are added at a closer distance in phrase 1.

In this phrase, relevant legislation and organisations which have a focus on reducing illegal/overfishing included as actions, as legislation is a way of inducing action. <a id="FAOfish">[FAO (2018)](#f8)</a> was used as a source of relevant legislation.

``` Ceylon =
TS=
(
  ("marine stewardship council"
  OR "regional fisheries management organi?ation$" OR "RFMOs"
  OR "UNCLOS" OR "convention on the law of the sea"
  OR "fish stocks agreement"
  OR "code of conduct for responsible fisheries" OR "CCRF"
  OR "port state measures agreement" OR "PSMA"
  OR "UNFSA" OR "Management of Straddling Fish Stocks" OR "Management of Highly Migratory Fish Stocks"
  OR "common fisheries policy"
  OR "law$" OR "legislation" OR "instrument$" OR "strateg*" OR "policy" OR "policies" OR "framework" OR "agreement*" OR "treaty" OR "treaties"
  OR "criminali*" OR "catch documentation" OR "surveillance" OR "regulation$" OR "regulated" OR "regulating" OR "enforc*"
  )
  NEAR/15
      ("overfish*"
      OR "bycatch" OR "by-catch"
      OR "IUU fishing"
      OR (("gear" OR "nets") NEAR/5 ("abandoned" OR "lost" OR "discarded"))
      OR "ghost fishing" OR "ghost nets" OR "ALDFG"
      OR
        (
          ("overharvest*" OR "overexploit*" OR "overcapacity" OR "collaps*" OR "closure$"
          OR "illegal*" OR "unreport*" OR "unregulated" OR "destructive" OR "blast" OR "dynamite" OR "cyanide"
          )
          NEAR/15 ("fishing" OR "fisher*" OR "shellfish*" OR "trawl*")
        )
      )       
)
```  

##### Phrase 3:

The basic structure is *action + management/restoration actions + fisheries*. This phrase differs to phrases 1 and 2 in that it focuses on sustainable management, rather than  overfishing or IUU fishing.

`management` will find a number of terms, e.g. "science-based management", "ecosystem based (fisheries) management" (EBFM), "area based management", "fisheries management policy" etc. Policies and frameworks which call for good management are included among the *action* terms; <a id="FAOfish">[FAO (2018)](#f8)</a> was used as a source of relevant legislation. Research about both the establishment and avoidance of fishery closures is considered to be relevant to implementing good management, as is research about the max. sustainable yield.

``` Ceylon =
TS=
(
  (
    ("implement*" OR "establish*" OR "introduc*" OR "adopt*" OR "design*" OR "propos*" OR "develop*"
    OR "reform*" OR "improv*" OR "better"     
    OR "law$" OR "legislation" OR "instrument$" OR "strateg*" OR "policy" OR "policies" OR "framework" OR "agreement*" OR "treaty" OR "treaties"      
    OR "marine stewardship council"
    OR "regional fisheries management organi?ation$" OR "RFMOs"
    OR "UNCLOS" OR "convention on the law of the sea"
    OR "fish stocks agreement"
    OR "code of conduct for responsible fisheries" OR "CCRF"
    OR "port state measures agreement"
    OR "UNFSA" OR "Management of Straddling Fish Stocks" OR "Management of Highly Migratory Fish Stocks"
    OR "common fisheries policy"
    )
    NEAR/15
      ("manage*" OR "plan" OR "planning" OR "governance"
      OR "restor*" OR "stock recovery"
      OR "sustainab*"
      OR "EBFM" OR "ecosystem approach*"
      OR "maximum sustainable yield*" OR "MSY"
      )
  )
  NEAR/15
      ("fishery" OR "fisheries" OR "fishing"
      OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
      OR "fish stock$" OR "overfishing"
      OR ("catch" NEAR/3 ("entitlement" OR "limit$" OR "tolerance$"))
      )
)
```
## Target 14.5

> **14.5 By 2020, conserve at least 10 per cent of coastal and marine areas, consistent with national and international law and based on the best available scientific information**
>
> 14.5.1 Coverage of protected areas in relation to marine areas

The target is interpreted to cover research about the establishment and management of marine protected areas. This provides overlap with 14.2 - while 14.2 is not explicitly about marine protected areas, "protect" is stated as one of the actions, suggesting that research on the establishment/maintenance of MPAs falls under 14.2 as well as 14.5.

This query consists of 1 phrase. The general structure is *action + protected areas*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**. The phrase is identical to 14.2 phrase 1.

Conserving areas of the ocean is considered widely to include several types of protected areas (which have different degrees of protection); for example, `no take zone$`, `conservation zone$`, `marine protected area$`. The phrase `"protect*" OR "conservation" NEAR/3 "area*" or "zone"` will cover "marine protected areas" and "marine conservation zones". For the action terms, I tested with `("increas*" NEAR/3 ("cover" OR "area" OR "size" OR "extent" OR "coverage"))` but it mostly gave noise.

``` Ceylon =
TS=
(
  ("designat*" OR "placement" OR "delineat*" OR "expand*" OR "extend"
  OR "design" OR "designing" OR "create" OR "creation" OR "creating" OR "develop" OR "development"
  OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e"
  OR "plans" OR "plan" OR "planned" OR "planning"
  OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "governance" OR "manag*"
  OR "enforce" OR "enforcement" OR "enforcing"
  OR "strengthen" OR "improv*"
  )
  NEAR/5
      ("MPA" OR "MPAs" OR "LSMPA$" OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
      OR "particularly sensitive sea area$"
      OR
        (
          ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving")
          NEAR/3 ("area$" OR "zone$" OR "habitat$" OR "ecosystem$")
        )
      OR ("no-take" NEAR/3 ("area$" OR "zone*" OR "reserve$")) OR "NTMR$"
      )
)
```

## Target 14.6

> **14.6 By 2020, prohibit certain forms of fisheries subsidies which contribute to overcapacity and overfishing, eliminate subsidies that contribute to illegal, unreported and unregulated fishing and refrain from introducing new such subsidies, recognizing that appropriate and effective special and differential treatment for developing and least developed countries should be an integral part of the World Trade Organization fisheries subsidies negotiation***
>
><sup>*Taking into account ongoing World Trade Organization negotiations, the Doha Development Agenda and the Hong Kong ministerial mandate.</sup>
>
>  14.6.1 Degree of implementation of international instruments aiming to combat illegal, unreported and unregulated fishing

This target is interpreted to cover research about reducing/eliminating fisheries subsidies that contribute to negative outcomes (overcapacity, overfishing, and IUU finishing). We also consider relevant research about development assistance and fisheries, and works talking about WTO and other instruments in the context of fisheries.

This query consists of 1 phrase. The general structure is *action + subsidies + fisheries // international instruments + fisheries*

`larval subsidi*` is a term to do with fish population dynamics and is removed.

``` Ceylon =
TS =
(
  (
    (
      ("reduc*" OR "limit" OR "minimi*"
      OR "prohibit*" OR "eliminat*" OR "ban" OR "banning" OR "banned" OR "cut*"
      OR "remov*" OR "end" OR "ending" OR "prevent*" OR "stop*" OR "halt*"
      )
      NEAR/5 "subsid*"
    )
    NEAR/15
        ("fishing" OR "fisher*" OR "overfishing"
        OR (("harvest*" OR "overcapacity") NEAR/15 ("fish*" OR "shellfish*"))
        )  
  )
  NOT "larval subsidi*"
)

OR

TS=
(
  ("ODA" OR "official development assistance" OR "doha development agenda" OR "hong kong ministerial" OR "world trade organization" OR "WTO")
  NEAR/15
      ("fishing" OR "fisher*" OR "overfishing"
      OR (("harvest*" OR "overcapacity") NEAR/15 ("fish*" OR "shellfish*"))
      )  
)
```

## Target 14.7

> **14.7 By 2030, increase the economic benefits to small island developing States and least developed countries from the sustainable use of marine resources, including through sustainable management of fisheries, aquaculture and tourism**
>
> 14.7.1 Sustainable fisheries as a proportion of GDP in small island developing States, least developed countries and all countries

This target is interpreted to include research about increasing economic benefits to LDCs and SIDS via sustainable use of marine resources. This target specifically only concerns least-developed countries and SIDS, but this is a bit inconsistent with the indicator which concerns all countries. This makes a large difference to the results. As the target is clearly focused on SIDS and LDCs, we retain this limit.

This query consists of 1 phrase. The general structure is *action + economic benefits + sustainable use/instruments + LDCs/SIDS*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

*economic benefits* is interpreted to also include e.g. livelihoods, blue growth, and ecosystem services. The `Nairobi Convention` is included, which refers to the Nairobi Convention for the Protection, Management, and Development of the Coastal and Marine Environment of the Eastern Africa region, as well as other instruments to do with sustainable use/fisheries.

``` Ceylon =
TS =
(
    (
      ("increase" OR "increasing" OR "increased" OR "increases"
      OR "strengthen*" OR "improv*" OR "restor*" OR "enhanc*" OR "better"
      OR "scal* up" OR "build* capacity" OR "capacity building"
      OR "expand" OR "expansion*" OR "develop" OR "developing" OR "development"
      OR "plans" OR "plan" OR "planned" OR "planning"
      OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "governance"
      )
      NEAR/5
          ("econom*" OR "GDP"
          OR "exploit*" OR "goods and services" OR "ecosystem service$"
          OR "socio economic" OR "socioeconomic"
          OR "livelihood$" OR "income$" OR "profit*"
          OR "trade" OR "trading" OR "market$"
          OR "monetary" OR "moneti*" OR "investor$"
          OR "bio-econom*" OR "bioeconom*"            
          OR "blue growth" OR "blue econom*" OR "blue bond$"
          )
    )
    AND
      ("sustainab*"
      OR "marine spatial planning" OR "MSP"
      OR "ecosystem based management" OR "ecosystem based fisheries management" OR "EBFM" OR "ecosystem approach"
      OR "area based management" OR "resilience based management" OR "community based management"
      OR "coastal zone management" OR "integrated coastal zone planning" OR "ICZM"
      OR "coastal resources management"
      OR "locally managed marine area$" OR "LMMA$"
      OR "marine protected area$" OR "MPA" OR "MPAs" OR "LSMPA$" OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
      OR "marine conservation zone$" OR "particularly sensitive sea areas$"
      OR "regional fisheries management organi?ation$" OR "RFMOs"
      OR "port state measures agreement"
      OR "fish stocks agreement" OR "UNFSA" OR "Management of Straddling Fish Stocks" OR "Management of Highly Migratory Fish Stocks"
      OR "code of conduct for responsible fisheries" OR "CCRF"
      OR "Nairobi Convention"
      )
    AND
      ("least developed countr*" OR "least developed nation$"  OR "small island developing state$" OR "Pacific island*"
      OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
      )
)

```

## Target 14.a

> **14.a Increase scientific knowledge, develop research capacity and transfer marine technology, taking into account the Intergovernmental Oceanographic Commission Criteria and Guidelines on the Transfer of Marine Technology, in order to improve ocean health and to enhance the contribution of marine biodiversity to the development of developing countries, in particular small island developing States and least developed countries**
>
> 14.a.1 Proportion of total research budget allocated to research in the field of marine technology

This target is difficult to interpret, particularly as "increase scientific knowledge [...] in order to improve ocean health" could cover just about all marine research. We interpret it to cover:
* research about biodiversity benefits to developing countries, LDCs and SIDS (phrase 1)
* research about transfer of marine technology, and improving marine research infrastructure/capacity (phrase 2 and 3)

This query consists of 3 phrases.

##### Phrase 1:

Concerns scientific knowledge about contributions of biodiversity to development. This includes diversity in terms of "economic" benefits (taken from 14.7), but also direct products of diversity, such as bioprospecting, new biotechnologies, genetic resources.

The general structure is *biodiversity benefits + developing countries*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

The `Nagoya protocol` is related to the convention on biological diversity (Nagoya Protocol on Access to Genetic Resources and the Fair and Equitable Sharing of Benefits Arising from their Utilization to the Convention on Biological Diversity).

``` Ceylon =
TS=
(
    ("blue growth" OR "blue econom*" OR "blue bond$"
    OR "bioprospect*"
    OR "biopiracy" OR "Nagoya protocol"
    OR ("bioactive$" NEAR/3 ("compound*" OR "substance*"))
    OR "bioresource$" OR "biological resource$" OR "genetic resource$"
    OR "biotechnolog*"
    OR
      (
        ("biodivers*" OR "diversity")
        NEAR/15
            ("sustainable development" OR "development intervention$" OR "human development" OR "social development" OR "development impacts" OR "development assistance"
            OR "tourism" OR "ecotourism" OR "tourist$" OR "sightsee*"
            OR "aquaculture" OR "fish farm*"
            OR "fisher*" OR "fishing" OR "harvest*" OR "aquarium trade"
            OR "exploit*" OR "goods and services" OR "ecosystem service$"
            OR "social ecological" OR "socialecological" OR "socioecological" OR "socio economic" OR "socioeconomic"
            OR "livelihood$"
            OR "profit*" OR "monetary" OR "monetiz*" OR "investor$"
            OR "econom*" OR "GDP"
            OR ("sustainab*" NEAR/5 ("utilization" OR "use" OR "using" OR "usage"))
            )
      )
    )
  AND
    (
      (("developing" OR "least developed")
      NEAR/3 ("state*" OR "nation$" OR "countr*" OR "small island*" OR "Pacific island*")
      )
      OR "Angola" OR "Benin" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Comoros" OR "Congo" OR "Djibouti" OR "Eritrea" OR "Ethiopia" OR "Gambia" OR "Guinea" OR "Guinea-Bissau" OR "Lesotho" OR "Liberia" OR "Madagascar" OR "Malawi" OR "Mali" OR "Mauritania" OR "Mozambique" OR "Niger" OR "Rwanda" OR "Sao Tome and Principe" OR "Senegal" OR "Sierra Leone" OR "Somalia" OR "South Sudan" OR "Sudan" OR "Togo" OR "Uganda" OR "Tanzania" OR "Zambia" OR "Cambodia" OR "Kiribati" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu" OR "Vanuatu" OR "Afghanistan" OR "Bangladesh" OR "Bhutan" OR "Nepal" OR "Yemen" OR "Haiti"
      OR "Antigua and Barbuda" OR "Antigua & Barbuda" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Comoros" OR "Cuba" OR "Dominica" OR "Dominican Republic" OR "Micronesia" OR "Fiji" OR "Grenada" OR "Guinea-Bissau" OR "Guyana" OR "Haiti" OR "Jamaica" OR "Kiribati" OR "Maldives" OR "Marshall Islands" OR "Mauritius" OR "Nauru" OR "Palau" OR "Papua New Guinea" OR "Saint Kitts and Nevis" OR "Saint Lucia" OR "St Lucia" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa" OR "Sao Tome" OR "Seychelles" OR "Singapore" OR "Solomon Islands" OR "Suriname" OR "Timor-Leste" OR "Tonga" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "Tuvalu" OR "Vanuatu" OR "Anguilla" OR "Aruba" OR "Bermuda" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia" OR "Guadeloupe" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia" OR "Niue" OR "Puerto Rico" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"
    )
)
```

##### Phrase 2:

Technology transfer - this is such a specific term, that any articles using it are likely to be highly relevant to the target.

The general structure is *transfer of technology*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

``` Ceylon =
TS=
(
  "transfer of marine technolog*"
  OR "marine technology transfer"
)
```

##### Phrase 3:

Concerns increasing scientific knowledge, research capacity and transfer of marine technology to improve ocean health. This phrase attempts to link various kinds of scientific and knowledge infrastructures to "ocean health" terms - a very broad concept. Research about advancing marine science in considered enough to be included.

The general structure is *action + marine science + ocean health/marine science*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

The IOC Criteria and Guidelines on Transfer of Marine Technology are relevant for this target, wherein marine technology includes information and data, guidelines, equipment for sampling, study and observation (both remote and in the lab), computer and modelling equipment/software, and expertise/skills in marine research (<a id="SDGindmetadata">[Statistics Division, 2021b (Indicator 14.a.1)](#f9)</a>).

The term `build*` in the first section covers capacity building. Some of the *ocean health* terms are taken from 14.2.

``` Ceylon =
TS=
(
    (
      ("share$" or "sharing" OR "provide"
      OR "develop*" OR "establish*" OR "build*" OR "implement*" OR "propos*" OR "design"
      OR "increas*" OR "improv*" OR "strengthen*" OR "enhanc*" OR "upgrade" OR "accelerate"
      OR "capacity development" OR "develop* capacity"  
      OR "invest" OR "investing"
      OR "joint research" OR "joint effort$" OR "collaborat*" OR "international cooperation"
      )
      NEAR/15
          ("ocean science" OR "ocean research" OR "marine research" OR "marine science"
          OR
            (
              ("research" OR "scientific" OR "science")
              NEAR/5
                  ("knowledge" OR "capacity"
                  OR "policy" OR "policies" OR "programme" OR "programmes" OR "research agenda" OR "framework$" OR "initiative$"
                  OR "advisor$"
                  OR "capabilit*" OR "training" OR "compentenc*" OR "expertise" OR "capabilit*" OR "skills"
                  OR "infrastructure" OR "facilities" OR "vessel$" OR "vehicle$" OR "laboratories" OR "laboratory facilities" OR "sampling equipment"
                  OR "database$" OR "software" OR "data"
                  OR "investment$" OR "funding" OR "GERD" OR "expenditure"
                  OR "network$"
                  )
            )
          OR "citizen science"
          OR "observ* network$" OR "observ* system$" OR "observ* facilities"
          OR "remote sensing equipment" OR "tide gauges"
          OR "data infrastructure$" OR "data network$" OR "ocean big data" OR "smart ocean" OR "modelling technique$"
          OR "monitoring network$" OR "biomonitoring"
          OR
            (
              ("ocean*" OR "marine" OR "biological" OR "ecological" OR "biodiversity" OR "environmental")
              NEAR/3 ("observator*" OR "monitoring")
            )
          OR
            (
              ("taxonom*" OR "genom*" OR "genetic" OR "species" OR "biodiversity" OR "diversity")
              NEAR/5
                  ("research" OR "capacity"
                  OR "knowledge" OR "data" OR "software"
                  OR "compentenc*" OR "expertise" OR "capabilit*" OR "skills"
                  OR "database$" OR "register$" OR "reference librar*" OR "inventory" OR "inventories" OR "information system$"
                  OR "guidelines"
                  OR "infrastructure$" OR "facilities" OR "sampling equipment" OR "laboratory facilities"
                  OR "herbaria" OR "museum collection$"
                  )            
            )
          )
    )
  AND
    ("marine life"
    OR (("ocean*" OR "marine") NEAR/3 ("research" OR "science" OR "scientific"))
    OR
      (
        ("ecosystem$" OR "habitat$" OR "environment*" OR "ocean$" OR "marine" OR "environment*")
        NEAR/3
            ("health$" OR "recovery"
            OR "service$" OR "functioning" OR "function$"
            OR "quality" OR "integrity" OR "stability" OR "resilience"
            )
      )
    OR "resilien*"
    OR "water quality"
    OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
    OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species"
    )
)
```

## Target 14.b

> **14.b Provide access for small-scale artisanal fishers to marine resources and markets**
>
> 14.b.1 Degree of application of a legal/regulatory/policy/institutional framework which recognizes and protects access rights for small-scale fisheries

This target is interpreted to cover research about the rights and governance of SSFs, as these shape access to resources and markets. It could be interpreted more narrowly to only cover research actually referring to access to marine resources/markets, but I feel this is too narrow here, as it is a small area and as "access" is controlled by many structures (governance, territorial control, common property...). This interpretation is supported as "Appropriate legal, regulatory and policy frameworks" are included as a key feature of an enabling environment for this indicator in the indicator metadata (<a id="SDGindmetadata">[Statistics Division, 2021b (Indicator 14.b.1)](#f9)</a>).

Should access to credit be included?

This query consists of 2 phrases.  Again, here, specific fish species as search terms are not needed because the focus is on fisheries (fisherpeople, fishermen, fishing, fishery, fisheries), NOT the biology of individual fish species (unless explicitly related by the authors to fisheries).

#### Phrase 1

The general structure is *fishing + small scale + access/rights/control*.

`use* right$` covers "territorial use rights in fisheries" (TURFs). `resource$` (under `access`) covers "marine resources".

``` Ceylon =
TS =
(
    (
      ("fisher*" OR "fishing" OR "shellfish" OR "marine resource$")
      NEAR/5 ("small-scale" OR "artisan*" OR "tradition*" OR "subsistence" OR "indigenous")    
    )
    AND
        (
          ("access"
          NEAR/5 ("fishery" OR "fisheries")
          )
        OR
          ("access*"
          NEAR/10
            ("ground$" OR "area$" OR "territor*"
            OR "resource$" OR "market$" OR "trade" OR "trader$" OR "commerc*"
            OR "conflict$" OR "dispute$" OR "contested" OR "competition"
            )
          )
        OR "territoriali*"
        OR
          (
            ("territor*" OR "boundaries")
            NEAR/5  
              ("fish*" OR "traditional" OR "restructur*" OR "planning"
              OR "conflict$" OR "dispute$" OR "contested" OR "appropriation$" OR "competition"
              )
          )
        OR
          (
            ("competition" OR "conflict$")
            NEAR/10 "fish*"
          )
        OR
          ("right$*"
          NEAR/5 ("fish*" OR "use" OR "usage" OR "property" OR "tenure" OR "territor*" OR "human" OR "lack of")
          )
        OR "ownership" OR "inheritance"
        OR "commons" OR "common property" OR "open access fish*"
        OR
          ("control$"
          NEAR/5 ("social" OR "catch" OR "state" OR "government" OR "legal" OR "commercial")
          )
        OR "equitab*" OR "inequitab*"
        OR "marginali*" OR "criminali*"
        OR "distributional justice" OR "blue justice" OR "blue injustice"
        )
)

```

#### Phrase 2

The general structure is *fishing + small scale + management/regulation*. `management` is not included in the first half with `traditional` because "traditional fisheries management" does not always refer to traditional fisheries, but the management traditions. Traditional is a word that is used in many contexts, thus `traditional` is also used with a closer near statement (in the first half).

```Ceylon =
TS =
(
    (
      ("fisher*" OR "fishing" OR "shellfish" OR "marine resource$")
      NEAR/5 ("small-scale" OR "artisan*" OR "tradition*" OR "subsistence" OR "indigenous")    
    )
    NEAR/5
        ("governance" OR "planning" OR "legislation" OR "policy" OR "policies" OR "framework" OR "law" OR "laws" OR "regulations")
)
OR
TS =
(
    (
      ("fisher*" OR "fishing" OR "shellfish" OR "marine resource$")
      NEAR/15 ("small-scale" OR "artisan*" OR "subsistence" OR "indigenous")    
    )
    NEAR/15 ("management" OR "governance" OR "planning" OR "legislation" OR "policy" OR "policies" OR "framework" OR "law" OR "laws" OR "regulations")
)
```

## Target 14.c

> **14.c Enhance the conservation and sustainable use of oceans and their resources by implementing international law as reflected in the United Nations Convention on the Law of the Sea, which provides the legal framework for the conservation and sustainable use of oceans and their resources, as recalled in paragraph 158 of “The future we want”**
>
> 14.c.1 Number of countries making progress in ratifying, accepting and implementing through legal, policy and institutional frameworks, ocean-related instruments that implement international law, as reflected in the United Nations Convention on the Law of the Sea, for the conservation and sustainable use of the oceans and their resources

This target is interpreted to cover research about the implementation and development of international law for conservation and sustainable use of the oceans.

This query consists of 2 phrases

##### Phrase 1
The general structure is *international law + action*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

This phrase contains specific international laws relevant to conservation and sustainable use. <a id="FAOfish">[FAO (2018)](#f8)</a> was used as a source of relevant legislation.

`CITES` is not included as it is also a verb.

``` Ceylon =
TS =
(
    ("law of the sea" OR "UNCLOS"
    OR "the future we want"
    OR (("biodivers*" OR "biological diversity" OR "fish*") NEAR/3 ("beyond national jurisdiction" OR "ABNJ"))
    OR "BBNJ"
    OR "common fisheries policy"
    OR "deep-sea fisheries guidelines" OR "Management of Deep-sea Fisheries in the High Seas"
    OR
      ("convention$"
      NEAR/3 ("Conservation of Antarctic Living Marine Resources" OR "biological diversity" OR "OSPAR" OR "international trade in endangered species")
      )
    OR
      ("directive$"
      NEAR/3 ("marine strategy framework" OR "water framework" OR "marine spatial planning")
      )
    OR "MSFD" OR "habitats directive"
    OR "regional seas programme"
    )
    NEAR/5
        ("implement*" OR "ratif*" OR "fulfill*"
        OR "ensur*" OR "enforc*" OR "into practice" OR "praxis"
        OR "develop*" OR "new" OR "propos*" OR "negotiat*"
        )
)
```

##### Phrase 2

The general structure is *sustinable use/conservation + international law + action*. **This phrase should be combined with [marine terms](https://github.com/SDGforskning/SDGstrings_wos/blob/main/SDG14_query_action_WoS.md#3-marine-terms-string-for-limiting-certain-phrases-to-the-marine-environment) with `AND`**.

Phrase 2 includes general phrases for international law, where sustainable use and conservation must be specified to prevent results about e.g. shipping/terretory disputes.  

``` Ceylon =
TS =
(
    ("conservation"
    OR "marine spatial planning" OR "MSP"
    OR "ecosystem based management" OR "area based management" OR "resilience based management"
    OR "coastal zone management" OR "integrated coastal zone planning" OR "ICZM"
    OR "coastal resources management"
    OR "community based management"
    OR "locally managed marine area$" OR "LMMA$"
    OR "MPA" OR "MPAs" OR "marine protected area$"
    OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
    OR "marine conservation zone$"
    OR "particularly sensitive sea areas$"
    OR "blue growth" OR "blue econom*"
    OR
      ("sustainab*"
      NEAR/5 ("manag*" OR "utilization" OR "use" OR "using" OR "usage")
      )
    OR
      ("sustainab*"
      NEAR/15
          ("manag*" OR "govern*"
          OR "tourism" OR "ecotourism" OR "tourist$"
          OR "aquaculture" OR "fish farm*"
          OR "fisher*" OR "fishing" OR "harvest*" OR "aquarium trade"
          OR "exploit*" OR "goods and services" OR "ecosystem services"
          OR "social ecological" OR "socialecological" OR "socioecological" OR "socio economic" OR "socioeconomic"
          OR "livelihood$"
          OR "profit*" OR "monetary" OR "monetiz*" OR "investor$"
          OR "econom*" OR "GDP"
          )
      )  
    )
  AND
    (
      ("international"
      NEAR/3 ("law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR "treaties" OR "framework$" OR "instrument$")
      )
      NEAR/5
          ("implement*" OR "ratif*" OR "fulfill*"
          OR "ensur*" OR "enforc*" OR "into practice" OR "praxis"
          OR "develop*" OR "new" OR "propos*" OR "negotiat*"
          )
    )  
)
```

## 5. Authorship and review

## 6. Footnotes

<a id="f6"></a> Aurora Universities Network. (2020). *Search Queries for “Mapping Research Output to the Sustainable Development Goals (SDGs)”* v5.0. [Dataset]. doi:10.5281/zenodo.3817445. [↩](#Aurora)

<a id="f8"></a> FAO. (2018). *The State of World Fisheries and Aquaculture 2018 - Meeting the sustainable development goals*. The State of World Fisheries and Agriculture. https://www.fao.org/documents/card/en/c/I9540EN/ [Accessed 03 December 2021].

<a id="f3"></a> Lloyd-Smith and Immig. (2018). *Ocean Pollutants Guide: Toxic Threats to Human Health and Marine Life*. International Pollutants Elimination Network/National Toxics Network.  https://ipen.org/sites/default/files/documents/ipen-ocean-pollutants-v2_1-en-web.pdf. [↩](#Marinepoll)

<a id="f5"></a> OECD. (2017). "Marine biodiversity, the role of marine protected areas and good practice insights" in *Marine protected areas: Economics, management and effective policy mixes*. https://doi.org/10.1787/9789264276208-en. [↩](#OECD)

<a id="f7"></a> Rivest, Maxime; Kashnitsky, Yury; Bédard-Vallée, Alexandre; Campbell, David; Khayat, Paul; Labrosse, Isabelle; Pinheiro, Henrique; Provençal, Simon; Roberge, Guillaume; James, Chris. (2021). *Improving the Scopus and Aurora queries to identify research that supports the United Nations Sustainable Development Goals (SDGs) 2021* V3. [Dataset]. doi: 10.17632/9sxdykm8s4.3 [↩](#Els)

<a id="f1"></a> Statistics Division. (2021a). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f9"></a> Statistics Division. (2021b). *SDG Indicators Metadata Repository*. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/metadata/ [accessed 8 December 2021] [↩](#SDGindmetadata)

<a id="f2"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/. [↩](#UNLDCs)

<a id="f4"></a> UN Environment Programme. (n.d.). *Addressing Land-Based Pollution*. United Nations. https://www.unep.org/explore-topics/oceans-seas/what-we-do/addressing-land-based-pollution [Accessed 22 November 2021]. [↩](#marinepollUN)
