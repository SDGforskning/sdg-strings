# Search query for SDG 15 - Life on Land, Bergen action-approach.
Protect, restore and promote sustainable use of terrestrial ecosystems, sustainably manage forests, combat desertification, and halt and reverse land degradation and halt biodiversity loss.

**Contents**

1. Full query
2. General notes
3. Terrestrial and freshwater terms
4. Documentation and string sections for each target
5. Contributions
6. Footnotes

## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here:  (no filters; publishing year = last 5 years): https://www.webofscience.com/wos/woscc/summary/9ea5875b-bc42-4d78-b83d-b09b380263ac-a7f65260/relevance/1

## 2. General notes

This document contains search strings for finding publications related to the **actions** in the SDG 15 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 15 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

SDG 15 is interpreted to be about ending environmental decline of terrestrial and inland freshwater ecosystems and restoring them. Special emphasis is on forests and the sustainable management of them, on wetlands, mountains and drylands, halting land degradation and desertification, protecting biodiversity, preventing the extinction of threatened species and the spreading of invasive alien species, as well as preventing wildlife trafficking. The consequences of ecosystem degradation and wildlife trafficking on human survival and well-being (e.g. spreading of zoonotic diseases) is included in UN SDG reports (<a id="Life2020">[SDG 15 Life on land](#f17)</a>; https://unstats.un.org/sdgs/report/2020/goal-15/; <a id="Life2021">[SDG 15 Life on land](#f18)</a>; https://unstats.un.org/sdgs/report/2021/goal-15/), but not specified in the targets.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[UN Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Abbreviations used:
* UN - United Nations
* DESA - Department of Economic and Social Affairs
* FAO - Food and Agriculture Organization
* CBD - Convention on Biological Diversity
* CITES - Convention on International Trade in Endangered Species of Wild Fauna and Flora

### What is life on *land*?

The attempt to limit the results to terrestrial and freshwater environments only (as opposed to marine) is made by combining the search strings with terrestrial and freshwater terms. However:

* In principle, the division between freshwater and marine is somewhat artificial for some species (e.g. migratory fish) or aquatic ecosystems; some habitats may span the marine and terrestrial environments (e.g. mangroves). These works should not be excluded.
* On a practical level, some habitats pose particular challenges for separating freshwater from marine, e.g. term `meadow` retrieves also articles about "seagrass meadows", `forests` about "kelp forests", and `coasts` can be marine coastal areas but also river delta coastal areas. 

We therefore attempt to limit to terrestrial or freshwater works, without being overly strict. This is mostly achieved by using two methods of combining the strings with terrestrial and freshwater terms - either directly with `AND` (works must mention a terrestrial term) or indirectly with `NOT marine` (which removes works mentioning marine terms unless a terrestrial term is also mentioned). See **Terrestrial and freshwater terms** below.

## 3. Terrestrial and freshwater terms: String for limiting certain phrases to the terrestrial and freshwater environment

This string is referred to as **terrestrial and freshwater terms** and is used in many of the strings below to limit the results to terrestrial and freshwater environment.

In some phrases, these terms are combined to the string with `AND` while in others a double `NOT` is used (`NOT marine NOT terrestrial/freshwater`). 
- Phrases which consist of more general terms are more likely to return results about topics irrelevant to the targets of SDG15 or natural environments, so these were combined with terrestrial/freshwater terms with `AND` to focus only on works which mention one of the terrestrial or freshwater terms. 
- Phrases which contain more specific ecological terms are more likely to already be focused on works about either marine, terrestrial or freshwater habitats/organisms, and only the pure marine works need to be excluded. `NOT marine NOT terrestrial/freshwater` was used for these as it excludes works using marine terms *unless* they also contain one of the terrestrial of freshwater terms. This "double NOT" strategy is commonly employed in the medical sciences to find human studies and exclude animal studies, while ensuring that animal studies are still included if they *also* mention humans. We use this strategy when possible as it has slightly better recall - for example, a work may be about a species of grass, but not use generic terms for terrestrial habitats - this work would likely be caught by the double `NOT` strategy, but be missed by the `AND` strategy. 

According to the SDG indicators metadata description for indicator 15.1.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-01-01.pdf) *mangroves* in tidal zones are included in forests regardless of whether this area is classified as land area or not, and are therefore included in our definition of "life on land".

Although mentioned in the definition for inland waters in the SDG indicator metadata for indicator 15.1.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-01-01.pdf), the terms `reservoirs` `canals` `dams` are not included in the string. Combined with management and water, they would be likely to bring many irrelevant results on water supply management etc.

Terms `land` and `fields` were initially in the phrase, but were removed to exclude many irrelevant results due to the broad meaning and use of these terms (e.g. scientific fields, magnetic field, Netherlands, England). `fells` are combined with Lapland because independently they brought a lot of noise (*fell* has many other meanings). Initially they were also combined with Scotland, but due to many irrelevant results, Scotland was left out. `heathland$` and `moorland$` are used rather than "heath" and "moor" because these words lead to a lot of irrelevant results (due to being names, typos in "health", historical groups).

```py
TS=
(
  "terrestrial" OR "soil" OR "soils"  
  OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$"
  OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal"
  OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$"
  OR "bush*" OR "shrub*" OR "meadow*" 
  OR "moorland$" OR "heathland$"
  OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe"
  OR "dryland$" OR "dry land" OR "desert*"
  OR "lowland$"
  OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$"
  OR "tundra"

  OR "freshwater" OR "limnic" OR "inland fish*"
  OR "lake*" OR "pond$"
  OR "river*" OR "stream$" OR "brook$" OR "creek$"
)
```

## 4. Targets

### Target 15.1

> **15.1 By 2020, ensure the conservation, restoration and sustainable use of terrestrial and inland freshwater ecosystems and their services,
> in particular forests, wetlands, mountains and drylands, in line with obligations under international agreements**
>
> 15.1.1 Forest area as a proportion of total land area
>
> 15.1.2 Proportion of important sites for terrestrial and freshwater biodiversity that are covered by protected areas, by ecosystem type

This target is interpreted to cover research about promoting a) conservation of terrestrial and inland freshwater ecosystems, b) restoring these ecosystems and c) using these ecosystems and their services sustainably. Sustainable management is understood to be a part of sustainable use.

Even though forests, wetlands, mountains and drylands are highlighted in the target description, they are not specified in the phrases since they are already included in the **Terrestrial and freshwater terms**, which are combined with all the phrases of this target either directly with `AND` or indirectly with `NOT marine` unless a terrestrial or freshwater habitat is mentioned.

This query consists of 5 phrases. 
* Phrases 1 and 2 cover protecting and restoring habitats and ecosystems. The phrases are similar, but differ in how strictly they are connected to **terrestrial or freshwater terms**. 
* Phrase 3 also covers research about protecting and restoring, but adds elements of management, for ecosystems, communities and biodiversity. 
* Phrase 4 covers implementation of sustainable management approaches for ecosystems and their services
* Phrase 5 aims to find research specifically related to the international agreements on conservation/restoration of terrestrial and freshwater ecosystems.

#### Phrase 1

This phrase aims to find research outputs about the establishment/management of protected areas for habitats and biotopes and promoting protection of habitats.

The elements of this phrase are *action + protected areas/conservation/restoration + habitats*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which lead to irrelevant results. Phrase 1 searches for protection of habitats limited only by the exclusion of marine habitats. Phrase 2 searches for conservation of ecosystems and more specific habitats. It is restricted more strictly to terrestrial habitats to exclude irrelevant results associated with the use of terms (e.g. `ecosystem`) on research areas other than natural sciences. 

While testing the phrases it was noticed that marine papers mentioning `seagrass meadows` will appear in the results for phrases 1 & 2 despite of the `NOT marine` string. They are brought by the term `meadow` in the terrestrial string. Irrelevant results are brought also by terms like `lake` and `river` when they appear in names of places.

```py
TS=
(
  ("designat*" OR "placement" OR "delineat*" OR "expand*" OR "extend"
  OR "design" OR "designing" OR "create" OR "creation" OR "creating" OR "develop" OR "development"
  OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e" OR "promote"
  OR "plans" OR "plan" OR "planned" OR "planning"
  OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "governance" OR "manag*"
  OR "enforce" OR "enforcement" OR "enforcing"
  OR "strengthen" OR "improv*"
  )
  NEAR/5
  ("protected area$" OR "Protected landscape$" OR "conservation area$" OR "conservation zone$" OR "Wilderness area$" OR "Nature reserve$" OR "National park$" 
    OR "Habitat management area$" OR "Species management area$"
    OR "conserv* ecosystem" OR "conserv* ecosystems" OR "protect* ecosystem" OR "protect* ecosystem$"
    OR
      (
        ("protect*" OR "preserve" OR "preservation" OR "preserved"
        OR "conserved" OR "conservation" OR "conserves" OR "conserving" OR "conserve"
        OR "reforest*" OR "rehabilit*" OR "restor*"
        )
        NEAR/5 ("habitat$" OR "biotope$")
      )
  )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research outputs about promoting protection of ecosystems and specific habitats. 

The elements of this phrase are *action + conservation/restoration + ecosystems/areas*. In order to specify to the terrestrial and freshwater ecosystems the phrase is combined with **Terrestrial and freshwater terms** with `AND`. Phrase 1 searches for protection of habitats limited only by the exclusion of marine habitats. Phrase 2 searches for conservation of ecosystems and more specific habitats. It is restricted more strictly to terrestrial habitats to exclude irrelevant results associated with the use of terms (e.g. `ecosystem`) on research areas other than natural sciences. 

While testing the phrases it was noticed that marine papers mentioning `seagrass meadows` will appear in the results for phrases 1 & 2 despite of the `NOT marine` string. They are brought by the term `meadow` in the terrestrial string. Irrelevant results are brought also by terms like `lake` and `river` when they appear in names of places.

```py
TS=
(
  ("designat*" OR "placement" OR "delineat*" OR "expand*" OR "extend"
  OR "design" OR "designing" OR "create" OR "creation" OR "creating" OR "develop" OR "development"
  OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e" OR "promote"
  OR "plans" OR "plan" OR "planned" OR "planning"
  OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "governance" OR "manag*"
  OR "enforce" OR "enforcement" OR "enforcing"
  OR "strengthen" OR "improv*"
  )
  NEAR/5
      (
        ("protect*" OR "preserve" OR "preservation" OR "preserved"
        OR "conserved" OR "conservation" OR "conserves" OR "conserving" OR "conserve"
        OR "reforest*" OR "rehabilit*" OR "restor*"
        )
        NEAR/5
          ("ecosystem$" OR "area*" OR "zone*" OR "environment*" 
          OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR "upland$" OR "tundra" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"
          )
      )
)
AND TS=("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
```

#### Phrase 3

This phrase aims to find research about restoring, protecting, conserving and managing terrestrial and freshwater ecosystems, species communities and biodiversity.

The action terms for this string are challenging because one can talk about "how to conserve the environment" (relevant), but could also just mention "the study was carried out in a conservation area" (less relevant). Therefore, we have action terms that are clear verbs for manage/protect etc., but combine other forms of these words with other actions (establishing, improving etc).

Under the ecosystems/elements, we include diversity at various levels (important for ecosystem functioning, resilience and services), key species and foundation species. As the use of term `ecosystem` by others than natural sciences brings irrelevant results, it was combined with terms refering to species and habitats.

The elements of this phrase are *action + conservation/restoration + ecosystems/diversity*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. Terms about human microbiome and terms which are related to diseases were added to `NOT` string in order to exclude articles about those. The medical terms were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

```py
TS=
(
  ("manage" OR "conserve" OR "protect" OR "restore"
  OR
    (
      ("designat*" OR "placement" OR "expand*" OR "extend"
      OR "design" OR "designing" OR "create" OR "creation" OR "creating"
      OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e" OR "promote"
      OR "plans" OR "plan" OR "planned" OR "planning" OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "strategy" OR "governance"
      OR "enforce" OR "enforcement" OR "enforcing"
      OR "increas*" OR "strengthen" OR "improv*" OR "enhance" OR "facilitat*"
      OR "preserv*" OR "support*" OR "ensur*"
      )
      NEAR/5 ("management" OR "conservation" OR "protection" OR "restoration" OR "sustainable")
    )
  )
  NEAR/15
      ("habitat$" OR "nature conservation"
      OR (("communit*") NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$"))
      OR (("ecosystem$" OR "diversity") NEAR/5 ("ecolog*" OR "species" OR "taxonom*" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR "upland$" OR "tundra" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")) 
      OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
      OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 4

This phrase aims to retrieve research about promoting sustainable use of terrestrial and freshwater ecosystems and their services. For better recall, some ecosystem services are specified, most of these found from the UN HLPF Background note for SDG 15 (<a>[UN-DESA/DSDG et al. 2018](#f4)</a>), UN topic page for Forests (<a id="forests">[UN DESA n.d.a](#f5)</a>) and SDG indicator metadata for indicator 15.3.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-03-01.pdf).

The elements of this phrase are *action + sustainability/sustainable use + natural resources/ecosystem services*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. `KBAs` are combined with a strign of species terms to exclude other meanings of the acronym KBA.

Some ecosystem services mentioned in indicator 15.3.1 metadata were not included in the phrase because they would be likely to return many results which are not relevant to the SDG 15:
* Cultural heritage
* Regional climate regulation
* Climate change mitigation
* Disaster risk reduction (flood, drought, soil erosion)
* Regulation of pests and diseases
* Water regulation
* Pollination
* Medicinal resources
* Primary production
* Nutrient cycling
* Water cycling
* Soil formation

```py
TS=
(
  ("promote" OR "enable" OR "increase" OR "establish" OR "implement*" OR "assure" OR "ensur*")
  NEAR/5
      ( "key biodiversity area$" OR "important sites for biodiversity" 
      OR "agro-ecological"
      OR "ecotourism"
      OR 
        (
          ("sustainab*" OR "responsibl*" OR "environmental*" OR "ecological*" OR "ecosystem approach")
          NEAR/5 ("grazing" OR "forestry" OR "fishing" OR "fisher*" OR "hunter$" OR "hunting" OR "trapping")
        )
      OR
        (
          ("long term management"
          OR
            (
              ("sustainab*" OR "responsibl*" OR "environmental*" OR "ecological*" OR "ecosystem approach")
              NEAR/5
                ("manag*" OR "use" OR "using" OR "development" 
                OR "govern*" OR "administrat*" OR "planning" OR "policies" OR "policy" OR "approach*" OR "strateg*"
                OR "recreation*" OR "tourism"
                OR "fuel wood" OR "fire wood" OR "firewood"
                )
            )
          )
          NEAR/15
                ("ecosystem service$" OR "natural resource$" OR "groundwater"
                OR "biodiversity" OR "biological diversity" OR "agrobiodiversity"
                OR "fisher*" OR "hunting" OR "trapping"
                OR "terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal"  OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"
                )
        )
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 5

This phrase aims to find research about promoting conservation/restoration of terrestrial and freshwater ecosystems specifically in relation to the international agreements or actions. Most of the agreements and treaties included by name are mentioned in the UN HLPF Background note SDG 15 (<a>[UN-DESA/DSDG et al. 2018](#f4)</a>). Two agreements concerning the use of genetic resources are included (*Nagoya Protocol* and *The Treaty on Plant Genetic Resources for Food and Agriculture*) assuming that mentioning these agreements in the context of terrestrial or freshwater habitats implies actions towards the targets of SDG 15.1.

The elements of this phrase are *action + international agreements/instruments*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. The term `CITES` is combined to a string of species terms (including particularly susceptable species from UN's World Wildlife Crime Report; <a id="wwc">[UNODC, 2020](#f13)</a>) in order to exclude irrelevant articles which use cite as a verb. The UN Convention on climate change `UNFCCC` is combined to a string of ecosystem terms to specify to conserving ecosystems (rather than reducing emissions in general).

```py
TS=
(
  ("promote" OR "enable" OR "increase" OR "establish*" OR "implement*" OR "assure"
  OR "introduc*" OR "adopt*" OR "integrate" OR "integrating" OR "design*" OR "propos*" OR "develop*"
  OR "ensur*" OR "enforc*" OR "ratif*" OR "fulfill*" OR "into practice" OR "praxis"
  OR "negotiat*" OR "reform*" OR "improv*" OR "better"
  OR "restore" OR "restored" OR "restoration"
  )
  NEAR/5
    (
      (
        ("international" NEAR/3 ("agreement$" OR "treat*"))
        NEAR/5
            ("ecosystem$" OR "habitat$" OR "environment*" OR "biotope$" OR "ecolog*"
            OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna"
            )
      )
    OR "Convention on Biological Diversity"
    OR ("CBD" NEAR/15 ("biological diversity" OR "biodiversity"))  
    OR "UN Convention to Combat Desertification" OR "United Nations Convention to Combat Desertification" OR "UNCCD"
    OR "Convention on International Trade in Endangered Species of Wild Fauna and Flora" 
    OR ("CITES" NEAR/15 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"))
    OR 
      (
        ("United Nations Framework Convention on Climate Change" OR "UN Framework Convention on Climate Change" OR "UNFCCC") 
        NEAR/15 ("ecosystem$" OR "habitat$" OR "environment*" OR "biotope$" OR "ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna")
      )
    OR "Nagoya Protocol"
    OR "Treaty on Plant Genetic Resources for Food and Agriculture" OR "International Seed Treaty" OR "Plant Treaty" OR "ITPGRFA"
    OR "Ramsar convention"
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.2

> **15.2 By 2020, promote the implementation of sustainable management of all types of forests, halt deforestation, restore degraded forests and substantially increase afforestation and reforestation globally**
>
> 15.2.1 Progress towards sustainable forest management

This target is interpreted to cover research about promoting sustainable forest management, reducing deforestation, and research which contributes to increasing forest covered land area globally. `Silvicultures` are included in the phrases because the SDG indicator metadata for indicator 15.1.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-01-01.pdf) does not limit forests to just natural ones. However including `arboricultures` is more debatable, by the indicator definition agricultural production systems (e.g. fruit tree or oil palm plantations) should not be included as forest for SDG 15. A machine learning algorithm "Random forests" brings irrelevant results not related to forests. Excluding these is not possible without missing relevant papers since "Random forests" can be applied also in forest research.

Specific forest management terms (methods, etc.) were found mainly from FAO’s Agrovoc thesaurus (<a id="agrovoc">[FAO, n.d.](#f15)</a>) and from a search query prepared in an earlier project for capturing forestry literature (<a id="stateforest">[Päivinen et al. (2021); International Status of Finnish Forest Research, Tapio research](#f16)</a>). 

This query consists of 3 phrases. Terrestrial and freshwater terms are **not** combined with the phrases 15.2.

#### Phrase 1

This phrase aims to find research about promoting sustainable forest management, with some of the management practices specified. The elements of this phrase are *action + sustainable use/practises/strategies & goals + forests*.

```py
TS=
(
  (
    ("promote" OR "enable" OR "increase" OR "establish*" OR "develop" OR "development"
    OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e" OR "promote"
    OR "restore" OR "restored" OR "restoration"
    OR "ensur*" OR "assure" OR "strengthen" OR "improv*"
    )
    NEAR/5
        ("sustainable forest*" OR "sustainable woodland$" OR "sustainable silvicultur*" OR "sustainable arboricultur*"
        OR
          (
            ("sustainabl*" OR "responsibl*" OR "environmental*" OR "ecological*")
            NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning" OR "policy" OR "policies" OR "strateg*" OR "approach*")
          )
        OR
          (
            ("sustainabl*" OR "responsibl*" OR "environmental*" OR "ecological*")
            NEAR/5
                ("practice$" OR "method$" OR "forestry operation$"
                OR "cutting" OR "cut" OR "logging" OR "felling" OR "clearing"
                OR "lopping" OR "*limbing" OR "thinning" OR "creaming" OR "pruning"
                OR "rotation"
                OR "regeneration" OR ("tree$" NEAR/3 "planting") 
                OR "drainage"
                OR "Forest area change"
                OR "Above-ground biomass in forest"
                OR ("proportion" NEAR/3 "protected areas")
                OR ("proportion" NEAR/3 "long-term management plan")
                OR "Forest under certification"
                OR "Certified forest area"
                )
          )
        OR (("protected" OR "reserved") NEAR/3 "forest*")
        OR "UN Strategic Plan for Forests" OR "UNSPF"
        OR "Global Forest Goals" OR "GFG$"
        )
  )
  NEAR/15 ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
)
```

#### Phrase 2

This phrase aims to find research about halting forest loss and degradation. The elements of this phrase are *action + deforestation/forest + loss**. 

REDD is not limited with action terms since REDD is an action itself (Reducing Emissions from Deforestation and forest Degradation).

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "avoid*" OR "prevent*" OR "combat*" OR "halt*" OR "resist*")
    NEAR/5
        ("deforest*"
        OR
          (
            ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
            NEAR/5 ("decreas*" OR "reduc*" OR "degrad*" OR "mitigat*" OR "disappear*" OR "lost" OR "loss")
          )
        )
  )
OR ("REDD" NEAR/15 ("UN" OR "United Nations" OR "*forest*"))
)
```

#### Phrase 3

This phrase aims to find research about increasing forest covered land area, and about promoting afforestation, reforestation and restoring degraded forests. The elements of the phrase are *action + cover/action + forest / action + forestation*.

```py
TS=
(
  (
    (
      (
        ("increas*" OR "expand*" OR "restore" OR "rehabilitate")
        NEAR/5 ("cover*" OR "area$" OR "zone$" OR "*land$" OR "silvicultur*")
      )
      OR "restore" OR "rehabilitate"
    )
    NEAR/5 ("*forest*" OR "woodland$")
  )
  OR
  (
    ("promot*" OR "prioriti*" OR "enabl*" OR "increase" OR "expand" OR "establish*" OR "implement*" OR "ensur*" OR "assure")
    NEAR/5
        ("afforest*" OR "reforest*"
        OR (("restor*" OR "rehabilita*") NEAR/5 ("*forest*" OR "woodland$"))
        )
  )
)
```

### Target 15.3

> **15.3 By 2030, combat desertification, restore degraded land and soil, including land affected by desertification, drought and floods, and strive to achieve a land degradation-neutral world**
>
> 15.3.1 Proportion of land that is degraded over total land area

This target is interpreted to cover research about:
- resisting desertifiction (phrase 1)
- restoring/maintaining land and soil quality in connection with floods, desertification and drought (phrase 2)
- reducing land and soil degredation (phrase 3)
- promoting land degradation neutrality (LDN) and maintenance of soil health (phrase 4) 

Definitions according to the SDG indicator metadata for indicator 15.3.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-03-01.pdf):
> "Land degradation is defined as the reduction or loss of the biological or economic productivity and complexity of rain fed cropland, irrigated cropland, or range, pasture, forest and woodlands resulting from a combination of pressures, including land use and management practices."

> "Land Degradation Neutrality (LDN) is defined as a state whereby the amount and quality of land resources necessary to support ecosystem functions and services and enhance food security remain stable or increase within specified temporal and spatial scales and ecosystems (decision 3/COP12)"

Given these definitions, we interpret the target to include research about all types of land (not just lands affected by desertification, drought or flooding). This means that these strings may pick up some works about soil erosion in built-up areas as well as "natural" areas. 

Sources used for definitions and specifying terms include: 
* 2018 UN HLPF Background note for SDG 15 (<a>[UN-DESA/DSDG et al. 2018](#f4)</a>) 
* CBD web pages for Dry and Sub-humid Lands (<a id="drylands">[CBD, Jun 2022](#f8)</a>)
* UN topic page for Desertification, Land degradation and Drought (<a id="desertification">[CBD, Jun 2022](#f6)</a>)

This query consists of 4 phrases. 

#### Phrase 1

This phrase aims to find research about resisting desertification. The elements of the phrase are *action + desertification // UN agreements to combat desertification*. We consider research mentioning specific instruments from the UN to be action orientated.

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending"
    OR "avoid*" OR "prevent*" OR "combat*" OR "tackle*" OR "halt*"
    OR "resist*" OR "reduc*" OR "decreas*" OR "minimi*"
    )
    NEAR/5
        ("desertif*"
        OR (("increas*" OR "expan*") NEAR/5 ("desert$" OR "dryland$"))
        )
  )
  OR "United Nations Convention to Combat Desertification"
  OR "UN Convention to Combat Desertification"
  OR "UNCCD"
)
```

#### Phrase 2

This phrase aims to find research about restoring/protecting land and soil health which has been affected by desertification, drought or floods. The elements of the phrase are *desertification/drought/flood + action + land or soil quality*.

In addition to articles about the effects agriforestry has on soils, this phrase also returns some articles about the effect of soil quality on agricultural productivity. These may still be concidered relevant to the target, since LDN by definition covers also land resources necessary for enhancing food security.

```py
TS=
(
  ("desert$" OR "desertif*" OR "drought$" OR "flood*" OR "dryland$")
  NEAR/15
      (
        ("restor*" OR "rehabilita*" OR "improv*" OR "enhanc*" OR "strengthen*"
        OR "maintain*" OR "preserv*" OR "conserv*" OR "protect*"
        )
        NEAR/15 ("soil structure" OR "soil fertility" OR "land fertility" OR "soil health" OR "soil productivity" OR "soil quality")
      )
)
```

#### Phrase 3

This phrase aims to find research about combating land degradation processes and effects. The elements of the phrase are *action + land degradation processes // action + effects of land degradation + land/soils*.

The terms for degradation processes are picked mainly from the SDG indicator metadata description for 15.3.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-03-01.pdf). Note that this phrase also finds a number of results about groundwater changes - we consider this a part of land/soil health. 

```py
TS=
(
  ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
  OR "avoid*" OR "prevent*" OR "combat*" OR "resist" OR "increas* resistance"
  OR "reduc*" OR "decreas*" OR "minimi*" OR "tackle*" OR "control"
  OR "restor*" OR "rehabilita*" OR "improv*" OR "enhanc*" OR "strengthen*"
  OR "maintain*" OR "preserv*" OR "conserv*" OR "protect*"
  )
  NEAR/5
      ("aridificat*"
      OR "soil pollution" OR "soil loss"
      OR
        (
          ("degrad*" OR "erosion" OR "eroded" OR "salinisat*"
          OR "alkalinisat*" OR "acidificat*" OR "contaminat*" OR "pollution"
          OR "biodiversity loss"
          )
          NEAR/5 ("land$" OR "soil$")
        )
      )
)
OR
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
    OR "avoid*" OR "prevent*" OR "combat*" OR "resist" OR "increas* resistance"
    OR "minimi*" OR "tackle*" OR "control"
    )
    NEAR/5
        (
          (
            ("decline" OR "decreas*" OR "reduc*" OR "degrad*" OR "lower$" OR "lowered" OR "lowering" OR "loss")
            NEAR/15
                ("biodiversity"
                OR ("vegetation" NEAR/3 ("cover" OR "communit*" OR "biomass"))
                OR ("soil$" NEAR/3 ("fertility" OR "quality"))
                )
          )
        OR (("chang*" OR "reduc*" OR "decreas*") NEAR/3 "groundwater")  
        )
  )      
  NEAR/15
      ("desertif*" OR "land degradation"
      OR (("arid" OR "semi arid" OR "semi-arid" OR "sub humid" OR "sub-humid") NEAR/3 ("area*" OR "land" OR "lands"))
      OR "soil$"
      )
)
```

#### Phrase 4

This phrase aims to find research about promoting land degradation neutrality (LDN) and protecting soil productivity/fertility. The elements of the phrase are *action + soil health/conservation // action + Land Degradation Neutrality*.

```py
TS=
(
  ("conserve" OR "protect" OR "preserve" OR "restore" OR "rehabilitate"
  OR "promoting" OR "promote" OR "improv*" OR "enhanc*" OR "strengthen*" OR "maintain*"
  )
  NEAR/5 
      ("soil" 
      NEAR/3 ("productivity" OR "fertility" OR "structure" OR "health" OR "protect*" OR "conserv*" OR "preserv*" OR "restor*" OR "rehabilita*")
      )
)
OR
TS=
(
  (
    ("promote" OR "prioriti*" OR "implement" OR "enable" OR "achiev*" OR "increase" OR "establish*"
    OR "restore" OR "restored" OR "restoration" OR "implement*" OR "assure" OR "ensur*"
    OR "policy" OR "policies" OR "framework$" OR "strateg*" OR "legislation"
    )
    NEAR/5 ("land degradation neutrality" OR "LDN")
  )
  AND "land degradation"
)
```

### Target 15.4

> **15.4 By 2030, ensure the conservation of mountain ecosystems, including their biodiversity, in order to enhance their capacity to provide benefits that are essential for sustainable development**
>
> 15.4.1 Coverage by protected areas of important sites for mountain biodiversity
>
> 15.4.2 Mountain Green Cover Index

This target is interpreted to cover research about conserving/managing/restoring and improving conservation/management/restoration for mountain ecosystems and their biodiversity. It is also considered to cover research about promoting the sustainable use of ecosystem services (benefits) provided by mountain ecosystems as defined on the UN topic page for Mountains (<a id="mountains">[UN DESA, n.d.c](#f5)</a>) in the context of sustainable development.

Specifying terms for the Mountain Green Cover Index are mentioned in the SDG metadata for indicator 15.4.2 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-04-02.pdf) and terms for Coverage by protected areas in the SDG metadata for indicator 15.4.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-04-01.pdf).

The phrases return some articles which mention `mountain` in a name of a species (e.g. Mountain hare, Mountain zebra, Mountain tapir). Some of these articles might not be about mountains, but identifying and excluding them without losing relevant articles would be quite challenging.

This query consists of 2 phrases. Terrestrial and freshwater terms are **not** combined with the phrases 15.4.

#### Phrase 1

This phrase aims to find research about conserving/managing/restoring and improving conservation/management/restoration of mountain ecosystems and their biodiversity. It includes research about establishing/managing protected areas, key biodiversity areas and vegetation covered areas of the mountains (Mountain Green Cover Index). 

Specifying terms for areas counted as green cover for the Mountain Green Cover Index `forest` `shrubs` `trees` `pasture` `cropland` `grassland` `wetland` are mentioned in the SDG metadata for indicator 15.4.2 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-04-02.pdf). `KBA` is not freely truncated due to noise from "kbar" (a unit).

The elements of this phrase are *(conserving OR action + management/conservation/protected areas/instruments) + ecosystem/biodiversity + mountains*

```py
TS=
(
  (
    ("manage" OR "conserve" OR "protect" OR "restore" OR "rehabilitate"
    OR
      (
        ("designat*" OR "placement" OR "expand*" OR "extend"
        OR "design" OR "designing" OR "create" OR "creation" OR "creating"
        OR "establish*" OR "propose*" OR "proposal$" OR "implement*" OR "prioriti$e" OR "promote"
        OR "plans" OR "plan" OR "planned" OR "planning" OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "strategy" OR "governance"
        OR "enforce" OR "enforcement" OR "enforcing"
        OR "increas*" OR "strengthen" OR "improv*" OR "enhance" OR "facilitat*"
        OR "preserv*" OR "support*" OR "ensur*"
        )
        NEAR/5
            ("manag*" OR "conserv*" OR "protect*" OR "restor*" OR "rehabilit*" OR "sustainable"
            OR "Protected area$" OR "Protected landscape$" OR "Wilderness area$" OR "Nature reserve$" OR "National park$" OR "Natural monument$" OR "Natural feature$"
            OR "Habitat management area$" OR "Species management area$"
            OR "key biodiversity area$" OR "KBA" OR "KBAs" OR "important sites for biodiversity"
            OR "Mountain Partnership"
            OR "Mountain Green Cover Index"
            OR "Convention on Biological Diversity" OR "CBD"
            OR "Convention on International Trade in Endangered Species of Wild Fauna and Flora" OR "CITES"
            )
      )
    )
    NEAR/15
        ("ecosystem$" OR "habitat$" OR "nature conservation"
        OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
        OR (("diversity" OR "communit*") NEAR/3 ("ecolog*" OR "species" OR "taxonom*" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
        OR ("cover*" NEAR/5 ("green" OR "vegetat*" OR "*forest$" OR "shrub$" OR "tree$" OR "pasture$" OR "cropland$" OR "grassland$" OR "wetland$"))
        )
  )
AND ("mountain*" OR "alpine" OR "highland$" OR ("fell$" NEAR/5 "Lapland") OR "montane")
)
```

#### Phrase 2

This phrase aims to find research about promoting sustainable use of the services/benefits provided by the mountain ecosystems. The elements of this phrase are *action + sustainable use + ecosystem services + mountains*

```py
TS=
(
  (
    (
      ("promot*" OR "enable" OR "increase" OR "establish*" OR "implement*" OR "ensur*")
      NEAR/5
          (
            ("sustainabl*" OR "environmental*" OR "ecological*" OR "ecosystem approach")
            NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning" OR "policy" OR "policies" OR "strateg*" OR "approach*")
          )
    )
    NEAR/15
        ("ecosystem$" OR "habitat$"
        OR (("communit*" OR "diversity") NEAR/5 ("ecolog*" OR "species" OR "taxonom*" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
        OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
        )
  )
  AND ("mountain*" OR "alpine" OR "highland$" OR ("fell$" NEAR/5 "Lapland") OR "montane")
)
```

### Target 15.5

> **15.5 Take urgent and significant action to reduce the degradation of natural habitats, halt the loss of biodiversity and, by 2020, protect and prevent the extinction of threatened species**
>
> 15.5.1 Red List Index

This target is interpreted to cover research about: 
- Reducing the degradation of terrestrial and freshwater habitats (phrase 1)
- Reducing the loss of biodiversity in these habitats (phrase 2)
- Conserving/managing or improving the management/conservation of biodiversity (phrase 3)
- Preventing extinction of threatened species (phrase 4)

All phrases of target 15.5. are combined with **Terrestrial and freshwater terms** either with `AND` or by excluding `marine` habitats, except when a **terrestrial or freshwater term is mentioned**. Because phrases 1 and 2 consist of more general terms, they are combined to **Terrestrial and freshwater terms** with `AND`. For phrases 3 and 4, which consist of terms used primarily in ecology, exclusion of `marine` habitats (except when a terrestrial or freshwater term is mentioned) and some other terms which were detected to bring irrelevant results was found sufficient.

This query consists of 4 phrases.

#### Phrase 1

This phrase aims to find research about reducing the degradation of terrestrial habitats. The elements of the phrase are *action + degratation + habitats*. 
In order to specify to the terrestrial and freshwater ecosystems the phrase is combined with **Terrestrial and freshwater terms** with `AND`.

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
    OR "avoid*" OR "prevent*" OR "combat*" OR "resist*" OR "tackle*"
    OR "reduc*" OR "decreas*" OR "minimi*"
    )
    NEAR/5 ("degrad*" OR "declin*" OR "loss" OR "lost" OR "destruct*" OR "disappear*" OR "fragmentat*")
  )
  NEAR/5
      ("ecosystem$" OR "habitat$" OR "biotope$"
      OR ("communit*" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      )
)
AND
TS=("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
```

#### Phrase 2

This phrase aims to find research about halting the loss of biodiversity. The elements of the phrase are *action + loss + biodiversity*. In order to specify to the terrestrial and freshwater ecosystems the phrase is combined with **Terrestrial and freshwater terms** with `AND`.

```py
TS=
(
  ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "avoid*" OR "prevent*" OR "combat*" OR "halt*" OR "resist*" OR "reduc*" OR "decreas*" OR "minimi*" OR "tackle*")
  NEAR/5
      (
        ("degrad*" OR "declin*" OR "loss" OR "lost" OR "destruct*" OR "disappear*")
        NEAR/5
            ("biodiversity" OR "biological diversity"
            OR (("diversity" OR "species") NEAR/5 ("species" OR "taxonom*" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
            )
      )
)
AND
TS=("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
```

#### Phrase 3

This phrase aims to find research about managing/conserving biodiversity.

The concept of *threatened species* is interpreted according to the classification of the SDG metadata for indicator 15.5.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-05-01.pdf): 
> "Threatened species are those listed on The IUCN Red List of Threatened Species in the categories Vulnerable, Endangered, or Critically Endangered (i.e., species that are facing a high, very high, or extremely high risk of extinction in the wild in the medium-term future)."

The elements of the phrase are *protecting / action + conservation/key biodiversity areas + biodiversity/threatened species*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. Terms about human microbiome and terms which are related to diseases were added to `double NOT` string in order to exclude articles about those. The medical terms were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

```py
TS=
(
  ("manage" OR "conserve" OR "protect" OR "restore" OR "promote" OR "rehabilitate"
  OR
    (
      ("promot*" OR "support*" OR "ensur*" OR "prioriti$e" OR "increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "facilitat*"
      OR "maintain*"
      OR "establish*" OR "propose*" OR "proposal$" OR "implement*"
      OR "plans" OR "plan" OR "planned" OR "planning" OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "strategy" OR "governance"
      )
      NEAR/5
          ("management" OR "conservation" OR "protection" OR "restoration" OR "rehabilitation"
          OR "key biodiversity area$" OR "KBA$"
          OR "important sites for biodiversity"
          )
    )
  )
  NEAR/5
      ("biodiversity" OR "biological diversity"
      OR ("diversity" NEAR/5 ("species" OR "taxonom*" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      OR (("threatened" OR "near extinct*" OR "at risk" OR "endanger*" OR "vulnerable" OR "protected" OR "red list*") NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$"))
      OR "Red List Index"
      OR "RLI" OR "Red List" OR "IUCN" OR "International Union for Conservation of Nature"
      )
)
NOT TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "microbiome$" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 4

This phrase aims to find research about preventing the extinction of threatened species. The elements of the phrase are *action + extinction + vulnerable/protected species*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
    OR "avoid*" OR "prevent*" OR "combat*" OR "resist*" OR "tackle*"
    OR "reduc*" OR "decreas*" OR "minimi*"
    )
    NEAR/5 ("extinction" OR "loss" OR "going extinct")
  )
  NEAR/15
        (
          ("threatened" OR "near extinct*" OR "at risk" OR "endanger*" OR "vulnerable" OR "protected" OR "red list*")
          NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$")
        )
)
NOT TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.6

> **15.6 Promote fair and equitable sharing of the benefits arising from the utilization of genetic resources and promote appropriate access to such resources, as internationally agreed**
>
> 15.6.1 Number of countries that have adopted legislative, administrative and policy frameworks to ensure fair and equitable sharing of benefits

This target is interpreted to cover research about improving sharing/access/fairness in relation to benefits of using a) genetic resources of terrestrial and freshwater organisms or their benefits, or b) traditional knowledge associated with these resources. 

Benefits are defined according to the CBD factsheet on Access and Benefit-Sharing (ABS) (<a id="abs">[CBD, n.d.](#f10)</a>). They range from basic research to development of products. By the definition of the CBD, benefit sharing applies also to benefits arising from the use of traditional knowledge of indigenous and local communities associated with genetic resources. *The Nagoya Protocol on Access to Genetic Resources and the Fair and Equitable Sharing of Benefits Arising from their Utilization to the Convention on Biological Diversity* is an essential agreement related to this target. CBD webpages on Nagoya protocol (<a id="nagoya">[CBD, Aug 2022](#f9)</a>) were used to define the aims and scope of this target.

In addition to papers about the use of terrestrial and freshwater resources, this query also returns some agricultural papers. They are not excluded from the results since the indicator 15.6.1 includes "Countries that are contracting Parties to the International Treaty on Plant Genetic Resources for Food and Agriculture (PGRFA)" (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-06-01.pdf).

This query consists of 3 phrases. The phrases are limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

This phrase aims to find research about promoting the sharing of genetic resources, including traditional knowledge of the indigenous and local communities. The elements of the phrase are *action + sharing/access + resources/knowledge + ecosystems/organisms/bioresources*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    (
      ("promot*" OR "improv*" OR "enhanc*" OR "strengthen*"
      OR "increas*" OR "expand*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
      )
      NEAR/5 ("share$" OR "sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$" OR "ownership" OR "appropriation" OR "biopiracy" OR "biocolonial*")
    )
    NEAR/15
        ("genetic resource$" OR "gene resources"
        OR ("knowledge" NEAR/3 ("traditional" OR "indigenous" OR "autochthonous" OR "local"))
        )
  )
  AND ("ecosystem$" OR "biotope$" OR "biodiversity" OR "biological diversity" OR "species" OR "plant*" OR "animal$" OR "organism$" 
      OR (("genetic resource$" OR "bioresource$" OR "biological resource$") NOT ("human" OR "patient$" OR "clinical" OR "protein" OR "microbiology")) 
      OR "gene resources"
      OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*"
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research about promoting the sharing of benefits derived from utilizing genetic resources. The elements of the phrase are *action + sharing/access + resources + benefits*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

While testing the phrase, it was noticed that `knowledge` combined with `local` or `traditional` brings some irrelevant results about various fields (transport, business, education).

```py
TS=
(
  (
    ("promot*" OR "improv*" OR "enhanc*" OR "strengthen*"
    OR "increas*" OR "expand*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
    )
    NEAR/5 ("share$" OR "sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$" OR "ownership" OR "appropriation" OR "biopiracy" OR "biocolonial*")
  )
  AND ("genetic resource$" OR "gene resource$")
  AND
      ("benefit$"
      OR ("results" NEAR/3 ("research" OR "development"))
      OR ("transfer*" NEAR/3 "technolog*")
      OR ("participat*" NEAR/3 "research activit*")
      OR ("develop*" NEAR/3 "product$")
      OR "fair compensation" OR "just compensation"
      OR "bioprospect*"
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 3

This phrase aims to find research about the instruments/treaties/agreements for promoting benefit sharing and access to genetic resources and traditional knowledge. The phrase is not limited by actions, since works mentioning the relevant international instruments/agreements are assumed to be related to promoting this target.

The elements of the phrase are *resources/knowledge + instruments*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  ("genetic resource$" OR "gene resource$*"
  OR ("knowledge" NEAR/3 ("traditional" OR "indigenous" OR "autochthonous" OR "local"))
  )
  NEAR/15
      ("Nagoya Protocol"
      OR "Convention on biological diversity" OR ("CBD" NEAR/15 ("biological diversity" OR "biodiversity"))
      OR "Access and benefit-sharing" OR "Access and benefit-sharing" OR "ABS"
      OR "Bonn Guidelines"
      OR "Plant Genetic Resources for Food and Agriculture" OR ("Plant Genetic Resources" NEAR/3 "FAO") OR "PGRFA"
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.7

> **15.7 Take urgent action to end poaching and trafficking of protected species of flora and fauna and address both demand and supply of illegal wildlife products**
>
> 15.7.1 Proportion of traded wildlife that was poached or illicitly trafficked

This target is interpreted to cover research about combatting poaching and trafficking of terrestrial and freshwater species. The target also covers the research about the markets or trade for illegal wildlife products. It is somewhat unclear to us whether the target aims to cover all poaching or just poaching of protected species. We have decided to include all species - in practice, many works talk about illegal trade/poaching in wildlife without specifically refering to "protected" species. 

Some particularly susceptible species were added to the phrase for better recall. The source for these was The UN's World Wildlife Crime Report (<a id="wwc">[UNODC, 2020](#f13)</a>).

This query consists of 3 phrases. The phrases are limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

This phrase aims to find research about ending poaching and trafficking of species. 

The elements of the phrase are *action + poaching/trafficking + species*. It is limited by the exclusion of marine habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results (particularly here, `traffick*` + `animal` is problematic in cell biology without NOT terms). 

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
    OR "prevent*" OR "combat*" OR "resist*" OR "tackle*"  
    OR "reduc*" OR "decreas*" OR "minimi*" OR "control*"
    OR "anti-poach*"
    )
    NEAR/5 ("poach*" OR "trafficking" OR "trafficked" OR "smuggl*")
  )
  NEAR/15
      ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" 
      OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"      
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "cell*" OR "*membrane*") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research about the markets/trade for illegal wildlife products. No action terms are combined with the markets (reduced demand & supply) because the phrase finds so few works if limited by action terms.

The elements of the phrase are *species + illegal products + markets*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" 
    OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"
    )
    NEAR/15
        (
          ("illegal*" OR "illicit*" OR "criminal" OR "crime")
          NEAR/5
              ("product$" OR "manufact*" OR "merchandise$" OR "artifact*" OR "fabricat*" OR "handicraft$" OR "handiwork$" OR "ivory"
              OR "market$*" OR "supply" OR "supplier$" OR "supplied" OR "demand" OR "trade" OR "trading" OR "import*" OR "export*" OR "purchas*" OR "livelihood$"
              )
        )
  )
  AND ("market$*" OR "supply" OR "supplier$" OR "supplied" OR "demand" OR "trade" OR "trading" OR "purchas*" OR "livelihood$")
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 3

This phrase aims to find research about protected/endangered species mentioning *The Convention on International Trade in Endangered Species of Wild Fauna and Flora (CITES)*. The elements of the phrase are *species + CITES*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

Action terms are not combined with this phrase since it could be assumed that articles mentioning protected/endangered species and CITES are action-oriented. Still, the phrase is quite broad and return also some articles which are more about target 15.5 (protection of threatened species) than about the trade on them. 

The term `CITES` is combined with a couple of NOT terms to try and remove "cite" as a verb. Even still, some such articles are retrived by this phrase. However, if `CITES` is combined, even with many species/animal terms, we lose many relevant works.

```py
TS=
(
  ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" 
  OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"
  )
  AND 
    ("Convention on International Trade in Endangered Species of Wild Fauna and Flora" 
    OR ("CITES" NOT ("article cites" OR "review cites" OR "author cites" OR "it cites" OR "work cites"))
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.8

> **15.8 By 2020, introduce measures to prevent the introduction and significantly reduce the impact of invasive alien species on land and water ecosystems and control or eradicate the priority species**
>
> 15.8.1 Proportion of countries adopting relevant national legislation and adequately resourcing the prevention or control of invasive alien species

This target is interpreted to cover research about preventing the introduction of alien species to terrestrial and freshwater ecosystems. It also covers research about reducing the impact of alien species, and controlling and eradicating them. The impacts are specified as defined in the SDG metadata for indicator 15.8.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-08-01.pdf).

By the definition of the Convention on Biological Diversity (CBD), from webpages from the CBD:
> "Invasive alien species are plants, animals, pathogens and other organisms that are non-native to an ecosystem, and which may cause economic or environmental harm or adversely affect human health" (<a id="aliens">[CBD, May 2021](#f11)</a>)

Not all alien species are invasive, and not all papers about invasive species necessarily mention the term alien. Terms `invasive` and `invasive alien` are sometimes used inconsistently. These phrases are designed to find research about preventing the introduction of any alien or invasive species to the ecosystems, and the negative impacts of them.

The phrases also return some papers about the effects of invasive species on agriculture (pests, diseases). By the CBD definition these might also be considered relevant (economic or environmental harm) even though they would not deal with the impacts on natural ecosystems.

All phrases return irrelevant medical papers (invasive disease/infection caused by a pathogen species/organism). Of the 100 checked results for each phrase, on average 2/100 were medical. These are hard to exclude, because (by the BCD definition) relevant papers may also be about the effects invasive alien species have on human health. Hence NOT disease etc. will exclude also relevant papers.

This query consists of 3 phrases. The phrases are limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

This phrase aims to find research about preventing the introduction/spread of alien/invasive species to ecosystems. The elements of the phrase are *action + introduction + alien species*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    ("prevent*" OR "combat*" OR "resist*" OR "tackle*" OR "reduc*" OR "decreas*" OR "minimi*" OR "control*")
    NEAR/5 ("introduct*" OR "spread*" OR "expansion" OR "dispers*" OR "range increase")
  )
  AND
      (
        ("invasive" OR "alien" OR "exotic" OR "nonnative" OR "non-native" OR "nonindigenous" OR "non-indigenous")
        NEAR/5 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "rodent$")
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research about reducing the impact of alien or invasive species on ecosystems. The elements of the phrase are *alien species + action + impact*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    ("invasive" OR "alien" OR "exotic" OR "nonnative" OR "non-native" OR "nonindigenous" OR "non-indigenous")
    NEAR/3 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "rodent$")
  )
  NEAR/15
      (
        ("reduc*" OR "resist*" OR "decreas*" OR "minimi*" OR "tackle*" OR "control*")
        NEAR/5
            ("impact*" OR "effect*" OR "affect*" OR "consequen*"
            OR "competition"
            OR "predation"
            OR "hybridisation"
            OR ("disease$" NEAR/3 ("transmission" OR "transmit*"))
            OR "parasitism"
            OR "trampling"
            OR "rooting"
            OR ("biodiversity" NEAR/3 ("loss" OR "lost"))
            OR ("habitat$" NEAR/3 "degrad*")
            OR ("ecosystem service$" NEAR/3 ("loss" OR "lost"))
            )
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 3

This phrase aims to find research about controlling and eradicating invasive or alien species. The elements of the phrase are *action + alien species*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  ("reduc*" OR "decreas*" OR "tackle" OR "control*" OR "eradicat*" OR "remov*")
  NEAR/5
      (
        ("invasive" OR "alien" OR "exotic" OR "nonnative" OR "non-native" OR "nonindigenous" OR "non-indigenous")
        NEAR/3 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "rodent$")
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.9

> **15.9 By 2020, integrate ecosystem and biodiversity values into national and local planning, development processes, poverty reduction strategies and accounts**
>
> 15.9.1 (a) Number of countries that have established national targets in accordance with or similar to Aichi Biodiversity Target 2 of the
> Strategic Plan for Biodiversity 2011–2020 in their national biodiversity strategy and action plans and the progress reported towards these targets;
> and (b) integration of biodiversity into national accounting and reporting systems, defined as implementation of the System of Environmental-Economic Accountings

This target is interpreted to cover research about national/local strategies/accounting/reporting and either a) ecosystem values/conserving ecosystems, b) conserving biodiversity, or c) the CBD Aichi Biodiversity Target 2 (CBD webpages; <a id="aichi">[CBD, Sep 2020](#f12)</a>). This covers research about national plans in context of *Aichi biodiversity targets* and *System of Environmental-Economic Accounting* which are mentioned in the SDG metadata for indicator 15.9.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-09-01.pdf). Biodiversity and ecosystem values are interpreted to be about protecting and conserving biodiversity and ecosystems. Even though the target specifies development processes and poverty reduction, `strategies` and `plans` in the phrases are not limited to just these. 

Articles about ecosystem and biodiversity values in national planning were assumed to be related to promoting the implementation of these. Hence, no action terms (such as promote/enable/etc.) were combined with the phrase of this target. 

This query consists of 1 phrase. The elements of this phrase are *NBSAPs // (Aichi/biodiversity values / conservation + ecosystem/biodiversity) + national/local + strategies*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results, e.g. `public health` `epidemiology` `national health` `healthcare` `health effects` `archaeology` `architecture*`. A set of medical terms about human microbiome and diseases was also added to exclude noise found in some cases when `diversity` is combined with `biological` etc. These were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

While testing the phrase it was noticed that the term `environment` will bring a lot noise due to its use on various fields (business environment, cultural environment, learning environment, etc.). To exclude these, `environment` was combined with a string of species & habitat terms.

```py
TS=
(
  ("National Biodiversity Strategy and Action Plan$"
  OR
    ("Aichi Biodiversity Target$" OR "Strategic Plan for Biodiversity" OR "ecosystem value$" OR "biodiversity value$" OR "nature conservation"
    OR
      (
        ("protect*" OR "conserv*" OR "improv*" OR "restor*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "support"
        )
        NEAR/5
            ("ecosystem$" OR "habitat$" OR "biotope$"
            OR (("communit*"  OR "environment*") NEAR/5 ("ecolog*" OR "biological" OR "biodiversity" OR "species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
            )
      )
    OR
      (
        ("protect*" OR "conserv*" OR "improv*" OR "restor*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "support" OR "promot*" OR "enhanc*" OR "increase"
        OR "System of Environmental-Economic Accounting" OR "SEEA"
        )
        NEAR/5
            ("biodiversity" OR "biological diversity"
            OR ("diversity" NEAR/5 ("ecolog*" OR "biological" OR "taxonom*" OR "species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
            )
      )
    )
  AND
    ("NBSAP$" OR "regional development"
    OR
      (
        ("national" OR "local" OR "government*" OR "regional" OR "sectoral" OR "municipal" OR "federal" OR "multilevel" OR "multi level"
        OR "urban" OR "settlement"
        OR "poverty reduction" OR "reduc* poverty" OR "anti poverty" OR "antipoverty"
        )
        NEAR/5
            ("target$" OR "goal$" OR "program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "governance"
            OR "plan" OR "planning" OR "plans" OR "action plan$" 
            OR "accounting" OR "reporting"
            )
      )
    )
  )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.a

> **15.a Mobilize and significantly increase financial resources from all sources to conserve and sustainably use biodiversity and ecosystems**
>
> 15.a.1 (a) Official development assistance on conservation and sustainable use of biodiversity; and (b) revenue generated and finance mobilized from biodiversity-relevant economic instruments

This target is interpreted to cover research about financing the conservation and sustainable use of biodiversity and ecosystems. 

Financial resources include development assistance and finance mobilized from economic instruments, including incentives mentioned in the SDG metadata for indicator 15.a.1  (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-0a-01.pdf) and financial instruments or capacity building initiatives mentioned in the HLPF Background note for SDG 15 (<a>[UN-DESA/DSDG et al. 2018](#f4)</a>).

We assume that all research about financial resources for conserving and sustainable use of biodiversity and ecosystem is relatively action-oriented. Hence, no additional action terms (such as increase, enhance, etc.) were combined with this query.

This query consists of 1 phrase. The elements of this phrase are *protection/sustainable use + ecosystem/biodiversity + financing/instruments*. The phrase is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. A set of medical terms about human microbiome and diseases was also added to exclude noise found in some cases when `diversity` is combined with `species` etc. These were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

As the use of term `ecosystem` by others than natural sciences brings irrelevant results (e.g. fintech ecosystems, startup ecosystems), it was combined with a string of species and habitat terms. Terms `community` `area` and `zone` were left out from the phrase in order to exclude irrelevant results.

```py
TS=
(
  (
    ("protect*" OR "conserv*" OR "restor*" OR "rehabilit*"
    OR "promot*" OR "improv*" OR "enhanc*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "support"
    OR
      (
        ("sustainabl*" OR "responsibl*" OR "environmental*" OR "ecological*")
        NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning")
      )
    )
    NEAR/15
        ("nature conservation" 
        OR ("ecosystem$" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")) 
        OR "ecosystem services" OR "ecosystem restoration"
        OR "habitat$" OR "biotope$"
        OR "biodiversity" OR "biological diversity"
        OR ("diversity" NEAR/5 ("species" OR "taxonom*" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$"))
        OR "Rio marker$"
        )
  )
  AND
      ("invest" OR "investing" OR "investment$" OR "financ*" OR "spending" OR "funding" OR "funder$" OR "fund$" OR "grant$"
      OR "financial support" OR "financial resources"
      OR
        (
          ("incentive$" OR "taxes" OR "tax" OR "fee$" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e")
          NEAR/5 ("biodiversity" OR "biological diversity")
        )
      OR "ODA" OR "cooperation fund$" OR "development spending"
      OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance"))
      OR "Global Environment Facility" OR "GEF"
      OR "Biodiversity Finance Initiative" OR "BIOFIN"
      OR "Partnership for Action on Green Economy" OR "PAGE"
      OR "Poverty-Environment Action for Sustainable Development" OR "Poverty Environment Action for Sustainable Development" OR "PEAS"
      OR "Green Commodities Programme"
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.b

> **15.b Mobilize significant resources from all sources and at all levels to finance sustainable forest management and provide adequate incentives to developing countries to advance such management, including for conservation and reforestation**
>
> 15.b.1 (a) Official development assistance on conservation and sustainable use of biodiversity; and (b) revenue generated and finance mobilized from biodiversity-relevant economic instruments

This target is interpreted to cover research about increasing financing/investments/incentives and either sustainable forest management, forest conservation or reforestation. This will cover research that considers both positive and negative effects of financing.

The elements of the phrase are *action + financing/incentives/instruments + sustainable use/conservation/reforestation + forests*. 

Part of the phrase (aiming for sustainable forest management) is similar to the 15.2 phrase 1, but the specified management practises are left out of the phrase to exclude results which might be less about sustainability and more about forestry as a business. Terms `planting trees` are added to this string, but not used in the strings of 15.2. In the context of this phrase these terms are likely to return relevant results. Whereas in the strings of 15.2 without the connection to incentives, they might bring noise.

```py
TS=
(
  (
    ("advanc*" OR "promot*" OR "improv*" OR "enhanc*" OR "strengthen*" OR "support"
    OR "increas*" OR "expand*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
    )
    NEAR/5 
        ("expenditure" OR "invest" OR "investing" OR "investment$" OR "financ*" OR "spending" OR "funding" OR "funder$" OR "fund$" OR "grant$"
        OR "financial support" OR "financial resources"
        OR "incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e" OR "payment$"
        OR "ODA" OR "cooperation fund$" OR "development spending"
        OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance"))
        )
  )
  AND
    (
      (
        ("sustainab*" OR "responsibl*" OR "environmental*" OR "ecological*")
        NEAR/5 
            ("manag*" OR "use" OR "using" OR "forestry" OR "practice$" OR "method$"
            OR "govern*" OR "development" OR "administrat*" OR "planning" OR "policy" OR "policies"
            OR "Forest area change" OR "Above-ground biomass in forest"
            )
      )
    OR
      (
        ("*forest*" OR "woodland$")
        NEAR/5 
            ("manag*" OR "govern*" OR "administrat*" OR "planning" OR "practice$" OR "policy" OR "policies"
            OR "restor*" OR "rehabilita*" OR "conserv*" OR "protect*" OR "maintain*" OR "preserv*"
            )
      )
    OR "Certified forest$" OR "Forest under certification" OR "forest certification"
    OR "long-term management plan*"
    OR "protected areas$" OR ("protected" NEAR/3 "forest*")
    OR  "forest reserves" OR ("reserved" NEAR/3 "forest*")
    OR "afforestr*" OR "reforestr*"
    OR (("planting" OR "plant") NEAR/3 "tree$")
    OR
      (
        ("increas*" OR "expand*")
        NEAR/5
            ("woodland$" OR "silvicultur*" OR "arboricultur*"
            OR ("*forest*" NEAR/3 ("cover*" OR "area$" OR "zone$" OR "*land$"))
            )
      )
    OR "UN REDD" OR "United Nations REDD" OR "REDD plus" OR "REDD+"
    OR "UN Strategic Plan for Forests" OR "UNSPF"
    OR "Global Forest Goals" OR "GFG$"
    )
  AND ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
)
```


### Target 15.c

> **15.c Enhance global support for efforts to combat poaching and trafficking of protected species, including by increasing the capacity of local communities to pursue sustainable livelihood opportunities**
>
> 15.c.1 Proportion of traded wildlife that was poached or illicitly trafficked

This target is interpreted to cover research about poaching and a) capacity and support (e.g. education, collaboration), or b) local communities or sustainable livelihoods. We settled on this interpretation as it covers a slightly more specific aspect than 15.7, which is more widely about combatting poaching. It is somewhat unclear to us whether the target aims to cover all poaching or just poaching of protected species. We have decided to include all species - in practice, many works talk about illegal trade/poaching in wildlife without specifically refering to "protected" species. 

This string is currently the same as the *topic approach* - no specific action terms are included. Works about e.g. "capacity building" are likely already quite action-oriented.

Some particularly susceptible species were added to the phrases for better recall. The source for these was The UN's World Wildlife Crime Report (<a id="wwc">[UNODC, 2020](#f13)</a>).

This query consists of 2 phrases. Both phrases are limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

The elements of the phrase are *capacity building/instruments + poaching/trafficking + protected species*. The phrase is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results  (particularly here, `traffick*` + `animal` is problematic in cell biology without NOT terms).

```py
TS=
(
  (
    ("capacity building" OR "capacity development" OR "capacity"
    OR "cooperation" OR "collaboration" OR "support" OR "international agreement$"
    OR "policy" OR "policies" OR "empower*" OR "invest" OR "investing" OR "investment$"
    OR "knowledge transfer*" OR "rais* awareness"
    OR (("poach*" OR "local") NEAR/3 ("awareness" OR "knowledge" OR "information"))
    OR "educat*"
    OR "Convention on International Trade in Endangered Species of Wild Fauna and Flora" OR "CITES"
    OR "Landscapes for People, Food and Nature partnership" 
    OR "anti poach* measures" OR "patrol$" OR "detection"
    )
    NEAR/15 ("poach*" OR "trafficking" OR "trafficked" OR "smuggl*" OR "illegal harvest*")
  )
  AND
    ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "mammals$"
    OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*" OR "cell*" OR "*membrane*") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research about poaching and trafficking of species in relation to sustainable livelihood opportunities of the local communities. `CITES` is added as an alternative to poaching or trafficking of species because often the implications to the local communities follow from the application of CITES decisions (<a id="cites">[CITES & General Secretariat of the Organization of American States, 2015](#f14)</a>).

The elements of the phrase are *CITES/poaching/trafficking + species + livelihoods/local communities*. The phrase is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned).

```py
TS=
(
  ("Convention on International Trade in Endangered Species of Wild Fauna and Flora"
  OR
    ("CITES"
    NEAR/5
        ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "mammals$"
        OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"
        )
    )
  OR
    (
      ("poach*" OR "trafficking" OR "trafficked" OR "smuggl*" OR "illegal harvest*")
      AND
        ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "mammals$"
        OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"
        )
    )
  )
  AND
      ("livelihood$" OR "employment"
      OR (("local" OR "indigenous" OR "rural" OR "native") NEAR/3 ("community" OR "communities" OR "people$"))
      OR
        (
          ("sustainable" OR "ecological" OR "legal" OR "eco friendly" OR "alternative$")
          NEAR/5 ("fishing" OR "fisher$" OR "hunt" OR "hunting" OR "hunter$" OR "*tourism" OR "agroforestry" OR "agriculture" OR "income")
        )
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*") NOT ("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle$" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "moorland$" OR "heathland$" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "steppe" OR "dryland$" OR "dry land" OR "desert*" OR "lowland$" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "upland$" OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

## 5. Contributions

* v1.0.0: Leena Byholm (Dec 2021-Sep 2022)

* Internal review: Caroline S. Armitage (May 2022, minor review Oct 2022)

* Testing v1.2.2: Project group; see documentation https://doi.org/10.5281/zenodo.8386611

* v2.0.0: Caroline S. Armitage (Aug-Sep 2023), minor review Håkon Magne Bjerkan.

Specialist input: Awaiting

## 6. Footnotes

<a id="f10"></a> CBD (n.d.). *Access and Benefit-Sharing (ABS)* [Factsheet]. https://www.cbd.int/abs/doc/protocol/factsheets/abs-en.pdf (Accessed 15 Aug. 2022). [↩](#abs)

<a id="f12"></a> CBD (edited Sep 2020). *Aichi Biodiversity Targets*. https://www.cbd.int/sp/targets/ (Accessed 15 Aug. 2022). [↩](#aichi)

<a id="f11"></a> CBD (edited May 2021). *What are Invasive Alien Species?*. https://www.cbd.int/idb/2009/about/what/ (Accessed 15 Aug. 2022). [↩](#aliens)

<a id="f8"></a> CBD (edited Jun 2022). *Dry and Sub-humid Lands Biodiversity*. https://www.cbd.int/drylands/  (Accessed 15 Aug. 2022). [↩](#drylands)

<a id="f9"></a> CBD (edited Aug 2022). *The Nagoya Protocol on Access and Benefit-sharing*. https://www.cbd.int/abs/ (Accessed 15 Aug. 2022). [↩](#nagoya)

<a id="f14"></a> CITES & General Secretariat of the Organization of American States (2015). *Handbook on CITES and livelihoods: Part II Addressing and mitigating the effects of the application of CITES decisions on livelihoods in poor rural communities*. United Nations. https://cites.org/sites/default/files/eng/prog/Livelihoods/Guia_PART2_CITES_ENG_FINAL.pdf. [↩](#cites)

<a id="f15"></a> FAO (n.d.). *AGROVOC Multilingual Thesaurus*. United Nations. https://agrovoc.fao.org/browse/agrovoc/en/page/c_16129  (Accessed 15 Aug. 2022). [↩](#agrovoc)

<a id="f5"></a> UN DESA (n.d.a). *Topics: Forests*. United Nations. https://sdgs.un.org/topics/forests (Accessed 15 Aug. 2022). [↩](#forests)

<a id="f6"></a> UN DESA (n.d.b). *Topics: Desertification, land degradation and drought*. United Nations. https://sdgs.un.org/topics/desertification-land-degradation-and-drought (Accessed 15 Aug. 2022). [↩](#desertification)

<a id="f5"></a> UN DESA (n.d.c). *Topics: Mountains*. United Nations. https://sdgs.un.org/topics/mountains (Accessed 15. Aug. 2022). [↩](#mountains)

<a id="f4"></a> UN DESA/DSDG et al. (2018). *2018 HLPF Review of SDGs implementation: SDG 15 - Protect, restore and promote sustainable use of terrestrial ecosystems, sustainably manage forests, combat deforestation and halt and reverse land degradation and biodiversity loss*. United Nations, Expert Group Meeting on Sustainable Development Goal 15: Progress and Prospects, New York. https://sdgs.un.org/sites/default/files/documents/196552018backgroundnotesSDG15.pdf

<a id="f13"></a> UNODC (2020). *World Wildlife Crime Report 2020: Trafficking in Protected Species*. United Nations. https://www.unodc.org/documents/data-and-analysis/wildlife/2020/World_Wildlife_Report_2020_9July.pdf. [↩](#wwc)

<a id="f17"></a> UN Statistics Division (2020). SDG 15 Life on land. https://unstats.un.org/sdgs/report/2020/goal-15/. [↩](#Life2020)

<a id="f1"></a> UN Statistics Division. (2021). *Global indicator framework for the Sustainable Development Goals and targets of the 2030 Agenda for Sustainable Development*. A/RES/71/313, E/CN.3/2018/2, E/CN.3/2019/2, E/CN.3/2020/2, E/CN.3/2021/2. Department of Economic and Social Affairs, United Nations. https://unstats.un.org/sdgs/indicators/Global%20Indicator%20Framework%20after%202021%20refinement_Eng.pdf [accessed 8 August 2021] [↩](#SDGT+Is)

<a id="f18"></a> UN Statistics Division (2021). SDG 15 Life on land. https://unstats.un.org/sdgs/report/2021/goal-15/. [↩](#Life2021)

<a id="f3"></a> UN Statistics Division (2022). SDG Indicators Metadata Repository. https://unstats.un.org/sdgs/metadata

<a id="f2"></a> United Nations. (2016, 2017, 2018, 2019, 2020, 2021). *World Economic Situation and Prospects; Statistical Annex*. https://www.un.org/development/desa/dpad/document_gem/global-economic-monitoring-unit/world-economic-situation-and-prospects-wesp-report/ [↩](#UNLDCs)

<a id="f16"></a> Päivinen, Risto; Petrokofsky, Gillian; Käär, Liisa; Harvey, William; Petrokofsky, Leo; Puttonen, Pasi; Kangas, Jyrki; Mikkola, Eero; Byholm Leena (2021) *International Status of Finnish Forest Research*. Tapio research. [Unpublished report] [↩](#stateforest)
