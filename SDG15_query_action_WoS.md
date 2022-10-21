
# Search query for SDG 15 - Life on Land, Bergen action-approach.

Protect, restore and promote sustainable use of terrestrial ecosystems, sustainably manage forests, combat desertification, and halt and reverse land degradation and halt biodiversity loss.

**Current status**: This string is currently a finished version (1.0.0).

**Contents**

1. Full query
2. General notes
3. Terrestrial and freshwater terms
4. Documentation and string sections for each target
5. Contributions
6. Footnotes

## 1. Full query

Results of the full search in its current state can be viewed on Web of Science by clicking here: https://www.webofscience.com/wos/woscc/summary/e2b0bb7a-4c43-488e-828b-427074731c30-57bfc5cc/relevance/1 (no filters; all years)

## 2. General notes

This document contains search strings for finding publications related to the **actions** in the SDG 15 targets and indicators ("action approach"; focus on precision, smaller result set). We also have a version which finds publications related to the topics in the SDG 15 targets and indicators ("topic approach"; focus on recall, larger result set), provided in the same repository as this file. For more explanation, see the Readme in this repository.

SDG 15 is interpreted to be about ending environmental decline of terrestrial and inland freshwater ecosystems and restoring them. Special emphasis is on forests and the sustainable management of them, on wetlands, mountains and drylands, halting land degradation and desertification, protecting biodiversity, preventing the extinction of threatened species and the spreading of invasive alien species, as well as preventing wildlife trafficking. The consequences of ecosystem degradation and wildlife trafficking on human survival and well-being (e.g. spreading of zoonotic diseases) is included in UN SDG reports (<a id="Life2020">[SDG 15 Life on land](#f17)</a>; https://unstats.un.org/sdgs/report/2020/goal-15/; <a id="Life2021">[SDG 15 Life on land](#f18)</a>; https://unstats.un.org/sdgs/report/2021/goal-15/), but not specified in the targets.

The attempt to limit the search to terrestrial and freshwater environments only (as opposed to marine) is made by combining the search strings with terrestrial and freshwater terms either directly with `AND` or indirectly with `NOT marine` – unless a terrestrial or freshwater term is mentioned (see **Terrestrial and freshwater terms** below). However, in aquatic ecosystems the division between freshwater and marine is sometimes artificial (e.g. migratory fish). Some habitats pose particular challenges for separating freshwater from marine, e.g. term `meadow` retrieves also articles about `seagrass meadows` and `coasts` can be marine coastal areas but also e.g. river delta coastal areas. According to the SDG indicators metadata description for indicator 15.1.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-01-01.pdf) mangroves in tidal zones are included in forests regardless of whether this area is classified as land area or not. Therefore, tight limiting to freshwater environments would leave out also relevant papers.

Targets and Indicators were found from the UN Statistics Division (<a id="SDGT+Is">[UN Statistics Division, 2021](#f1)</a>). This list includes "the global indicator framework as contained in A/RES/71/313, the refinements agreed by the Statistical Commission at its 49th session in March 2018 (E/CN.3/2018/2, Annex II) and 50th session in March 2019 (E/CN.3/2019/2, Annex II), changes from the 2020 Comprehensive Review (E/CN.3/2020/2, Annex II) and refinements (E/CN.3/2020/2, Annex III) from the 51st session in March 2020, and refinements from the 52nd session in March 2021 (E/CN.3/2021/2, Annex)". (https://unstats.un.org/sdgs/indicators/indicators-list/)

Abbreviations used:
* UN - United Nations
* DESA - Department of Economic and Social Affairs
* FAO - Food and Agriculture Organization
* CBD - Convention on Biological Diversity
* CITES - Convention on International Trade in Endangered Species of Wild Fauna and Flora

## 3. Terrestrial and freshwater terms: String for limiting certain phrases to the terrestrial and freshwater environment

This string is referred to as **terrestrial and freshwater terms**, and is used in sets **15.1, 15.5, 15.6, 15.7, 15.8, 15.9, 15.a** and **15.c** to limit the results to terrestrial and freshwater environment.

In some phrases, these terms are combined to the string with `AND` while in others a double `NOT` is used (`NOT marine NOT terrestrial/freshwater`). 
- Phrases which consist of more general terms are more likely to return results about topics irrelevant to the targets of SDG15 or natural environments, so these were combined with terrestrial/freshwater terms with `AND` to focus only on works which mention one of the terrestrial or freshwater terms. 
- Phrases which contain more specific ecological terms are more likely to already be focused on works about either marine, terrestrial or freshwater habitats/organisms, and only the pure marine works need to be excluded. `NOT marine NOT terrestrial/freshwater` was used for these as it excludes works using marine terms *unless* they also contain one of the terrestrial of freshwater terms. This "double NOT" strategy is commonly employed in the medical sciences to find human studies and exclude animal studies, while ensuring that animal studies are still included if they *also* mention humans. We use this strategy when possible as it has slightly better recall - for example, a work may be about a species of grass, but not use generic terms for terrestrial habitats - this work would likely be caught by the double `NOT` strategy, but be missed by the `AND` strategy. 

The term `mangrove` is added only when the string is used with `NOT marine`.

Although mentioned in the definition for inland waters in the SDG indicator metadata for indicator 15.1.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-01-01.pdf), the terms `reservoirs` `canals` `dams` are not included in the string. Combined with management and water, they would be likely to bring many irrelevant results on water supply management etc.

Terms `land` and `fields` were initially in the phrase, but were removed to exclude many irrelevant results due to the broad meaning and use of these terms (e.g. *scientific fields, magnetic field, Netherlands, England*).

`fells` are combined with Lapland because independently they brought a lot of noise (*fell* has many other meanings). Initially they were also combined with Scotland, but due to many irrelevant results, Scotland was left out.

```py
TS=
(
  "terrestrial" OR "soil" OR "soils"  
  OR "*forest*" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$"
  OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal"
  OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$"
  OR "bush*" OR "shrub*" OR "meadow*"
  OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$"
  OR "dryland$" OR "dry land" OR "desert*"
  OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland")
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

This query consists of 5 phrases. Phrases 1 and 2 cover research about estblishing protected areas and promoting protection of habitats and ecosystems. Phrase 1 searches for protection of habitats limited only by the exclusion of marine habitats. Phrase 2 searches for conservation of ecosystems and more specific habitats. It is restricted more strictly to terrestrial habitats to exclude irrelevant results associated with the use of terms (e.g. `ecosystem`) on research areas other than natural sciences. Phrase 3 covers research about restoring, protecting, conserving and managing ecosystems, species communities and biodiversity. Phrase 4 covers the implementing of sustainable management approaches. Phrase 5 aims to find research specifically related to the international agreements on conservation/restoration of terrestrial and freshwater ecosystems.

While testing the phrases it was noticed that marine papers mentioning `seagrass meadows` will appear in the results for phrases 1 & 2 despite of the `NOT marine` string. They are brought by the term `meadow` in the terrestrial string. Irrelevant results are brought also by terms like `lake` and `river` when they appear in names of places.

#### Phrase 1

This phrase aims to find research outputs about the establishment/management of protected areas for habitats and biotopes and promoting protection of habitats. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

The elements of this phrase are *action + protection/protected areas + habitats*.

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
	    ("protected area$" OR "conservation area$" OR "conservation zone$" OR "Wilderness area$" OR "Nature reserve$" OR "National park$" OR "Habitat management area$" OR "Species management area$" OR "Protected landscape$"
	    OR "conserv* ecosystem" OR "conserv* ecosystems" OR "protect* ecosystem" OR "protect* ecosystem$"
	    OR
	      (
        	("protect*" OR "preserve" OR "preservation" OR "preserved"
        	OR "conserved" OR "conservation" OR "conserves" OR "conserving" OR "conserve"
       		OR "reforest*" OR "rehabilit*"
        	)
          NEAR/5 ("habitat$" OR "biotope$")
	      )
	    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research outputs about promoting protection of ecosystems and specific habitats. 

The elements of this phrase are *action + protect + ecosystem/habitats/areas*. In order to specify to the terrestrial and freshwater ecosystems the phrase is combined with **Terrestrial and freshwater terms** with `AND`.

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
        OR "reforest*" OR "rehabilit*"
        )
        NEAR/5
          ("ecosystem$" OR "area*" OR "zone*" OR "environment*" OR "woodland$" OR "forest$" OR "taiga" OR "peatland$" OR "bog$"
          OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" 
          OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*"
          OR "highland$" OR "alpine*" OR "tundra" OR "limnic" OR "lake*" OR "pond$" OR "river*" OR "stream$"
          )
      )
)
AND TS=("terrestrial" OR "soil" OR "soils" OR "forest$" OR "woodland$" OR "taiga" OR "jungle" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
```

#### Phrase 3

This phrase aims to find research about restoring, protecting, conserving and managing terrestrial and freshwater ecosystems, species communities and biodiversity.

The action terms for this string are challenging because one can talk about "how to conserve the environment" (relevant), but could also just mention "the study was carried out in a conservation area" (less relevant). Therefore, we have action terms that are clear verbs for manage/protect etc., but combine other forms of these words with other actions (establishing, improving etc).

Under the ecosystems/elements, we include diversity at various levels (important for ecosystem functioning, resilience and services), key species and foundation species.

As the use of term `ecosystem` by others than natural sciences brings irrelevant results, it was combined with terms refering to species and habitats.

The elements of this phrase are *action + ecosystems/elements*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. Terms about human microbiome and terms which are related to diseases were added to `NOT` string in order to exclude articles about those. The medical terms were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

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
      NEAR/5
          ("management" OR "conservation" OR "protection" OR "restoration" OR "sustainable")
    )
  )
  NEAR/15
      ("habitat$"
      OR ("ecosystem$" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")) 
      OR ("communit*" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$"))
      OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
      OR ("diversity" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
      ("long term management plan"
      OR "agro-ecological knowledge" OR "agro ecological knowledge"
      OR "bidiversity" OR "biological diversity"
      OR "key biodiversity area$" 
      OR ("KBA$" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR 	"tree$" OR "grassland$" OR "pollinator$"))
      OR "important sites for biodiversity"
      OR "biodiversity of food systems" OR "agrobiodiversity"
      OR "soil biodiversity"
      OR "ecotourism"
      OR (("sustainab*" OR "responsible") NEAR/5 ("ecosystem service$" OR "natural resource$" OR "soil" OR "freshwater" OR "groundwater"))
      OR
        (
          (
            ("sustainab*" OR "responsibl*" OR "environmental*" OR "ecological*" OR "ecosystem approach")
            NEAR/3
              ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning"
              OR "fishing" OR "fisher*" OR "hunter$" OR "hunting" OR "trapping"
              OR "forestry"
              OR (("recreation*" OR "tourism") NEAR/5 ("nature" OR "ecologic*"))
              OR "grazing"
              OR "fuel wood" OR "fire wood" OR "firewood"
              )
          )
          NEAR/15
              ("ecosystem service$" OR "natural resource$" OR "groundwater"
              OR "fisher*" OR "game" OR "forest$"
              OR "terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"
              )
        )
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
            NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning" OR "policy" OR "policies")
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
          OR ("protected" NEAR/3 "forest*")
          OR ("reserved" NEAR/3 "forest*")
          OR "UN Strategic Plan for Forests" OR "UNSPF"
          OR "Global Forest Goals" OR "GFG$"
          )
  )
  NEAR/15 ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
)
```

#### Phrase 2

This phrase aims to find research about halting forest loss and degradation. The elements of this phrase are *action + forests + loss*. 

REDD is not limited with action terms since REDD is an action itself (Reducing Emissions from Deforestation and forest Degradation).

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "avoid*" OR "prevent*" OR "combat*" OR "halt*" OR "resist*")
    NEAR/5
        ("deforest*"
        OR ("*forest*" NEAR/3 ("loss" OR "degrad*"))
        OR ("lost" NEAR/3 "forest area")
        OR
          (
            ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
            NEAR/5 ("decreas*" OR "reduc*" OR "degrad*" OR "mitigat*" OR "disappear*" OR "lost" OR "loss")
          )
        )
  )
OR ("REDD" NEAR/15 ("UN" OR "United Nations"))
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
        ("increas*" OR "expand*" OR "restor*" OR "rehabilitate")
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
        ("afforestr*" OR "reforestr*"
        OR (("restor*" OR "rehabilita*") NEAR/5 ("*forest*" OR "woodland$"))
        )
  )
)
```

### Target 15.3

> **15.3 By 2030, combat desertification, restore degraded land and soil, including land affected by desertification, drought and floods, and strive to achieve a land degradation-neutral world**
>
> 15.3.1 Proportion of land that is degraded over total land area

This target is interpreted to cover research about resisting desertifiction and about restoring land and soil that has been degraded by desertification, drought or floods. It also covers research which contributes to achieving land degradation neutrality (LDN). Land degradation neutrality is defined in the SDG indicator metadata for indicator 15.3.1:
> "a state whereby the amount and quality of land resources necessary to support ecosystem functions and services and enhance food security remain stable or increase within specified temporal and spatial scales and ecosystems" (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-03-01.pdf).

It is somewhat unclear to us whether the phrases should cover all land degradation or just land degradation related to deserification, drought and floods. Our interpretation on this is done separetely for each phrase. Phrase 2 is more tightly limited to searching for lands degraded by desertification, drought or floods, whereas phrase 3 includes the degradation of all lands. Phrase 4 is limited only to drylands conserning soil productivity but to all lands conserning LDN. 

Sources used for definitions and specifying terms for deserts and drylands (in phrases 3 & 4): 
* 2018 UN HLPF Background note for SDG 15 (<a>[UN-DESA/DSDG et al. 2018](#f4)</a>) 
* CBD web pages for Dry and Sub-humid Lands (<a id="drylands">[CBD, Jun 2022](#f8)</a>)
* UN topic page for Desertification, Land degradation and Drought (<a id="desertification">[CBD, Jun 2022](#f6)</a>)

This query consists of 4 phrases. Terrestrial and freshwater terms are **not** combined with the phrases 15.3.

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
        OR (("increas*" OR "expand*") NEAR/5 ("desert$" OR "dryland$"))
        )
  )
  OR "United Nations Convention to Combat Desertification"
  OR "UN Convention to Combat Desertification"
  OR "UNCCD"
)
```

#### Phrase 2

This phrase aims to find research about restoring land and soil which has been degraded by desertification, drought or floods. The elements of the phrase are *desertification/drought/flood + action + degraded land or soils*.

In addition to articles about the effects agriforestry has on soils, this phrase also returns some articles about the effect of soil quality on agricultural productivity. These may still be concidered relevant to the target, since LDN by definition covers also land resources necessary for enhancing food security.

```py
TS=
(
  ("desert$" OR "desertif*" OR "drought" OR "flood$" OR "dryland$")
  NEAR/15
      (
        (
          ("restor*" OR "rehabilita*" OR "improv*" OR "enhanc*" OR "strengthen*")
          NEAR/5
              (
                ("degrad*" NEAR/3 ("land$" OR "soil$"))
                OR (("erosion" OR "eroded") NEAR/5 ("land$" OR "soil$"))
              )
        )
      OR
        ("restor*" OR "rehabilita*" OR "improv*" OR "enhanc*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "conserv*" OR "protect*")
        NEAR/15
            ("soil structure" OR "soil fertility" OR "soil health"
            OR ("quality" NEAR/5 ("soil$" OR "land"))
            )
      )
)
```

#### Phrase 3

This phrase aims to find research about combating land degradation processes and effects. The terms for degradation processes are picked mainly from the SDG indicator metadata description for 15.3.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-03-01.pdf).

The elements of the phrase are *action + land degradation processes OR action + effects of land degradation + deserts/drylands/soils*.

```py
TS=
(
  ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
  OR "avoid*" OR "prevent*" OR "combat*" OR "resist" OR "increas* resistance"
  OR "reduc*" OR "decreas*" OR "minimi*" OR "tackle*" OR "control"
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
        OR (("chang*" OR "reduc*" OR "decreas*") NEAR/3 ("groundwater" NEAR/3 ("level$" OR "quality")))  
        )
  )      
  NEAR/15
      ("desert$" OR "desertif*" OR "dryland$" OR "dry land$"
      OR (("arid" OR "semi arid" OR "semi-arid" OR "sub humid" OR "sub-humid") NEAR/3 ("area*" OR "land*"))
      OR "grassland$" OR "savanna$" OR "prairie$" OR "rangeland$"
      OR "soil$"
      )
)
```

#### Phrase 4

This phrase aims to find research about promoting land degradation neutrality (LDN) in all lands, and protecting land productivity in drylands. There is uncertainty about whether this phrase should cover LDN on drylands only, and whether land productivity should be covered for all lands of limited to drylands only. The phrase is now limited only to drylands when searching for soil productivity but to all lands when searching for LDN. 

The elements of the phrase are *deserts/drylands + action + land productivity OR action + Land Degradation Neutrality*.

```py
TS=
(
  ("desert$" OR "desertif*" OR "dryland$" OR "dry land$"
  OR (("arid" OR "semi arid" OR "semi-arid" OR "sub humid" OR "sub-humid") NEAR/3 ("area*" OR "land*"))
  OR "grassland$" OR "savanna$" OR "prairie$" OR "rangeland$"
  )
  NEAR/15
      (
        ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving"
        OR "promoting" OR "promote" OR "improv*" OR "restor*" OR "enhanc*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "support"
        )
        NEAR/15 (("soil" OR "land") NEAR/3 ("productivity" OR "fertility"))
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

This target is interpreted to cover research about conserving and improving conservation of mountain ecosystems and their biodiversity. We consider conservation to also cover research about management, restoration and protection of these. It is also considered to cover research about promoting sustainable use of ecosystem services (benefits) provided by mountain ecosystems as defined on the UN topic page for Mountains (<a id="mountains">[UN DESA, n.d.c](#f5)</a>) in the context of sustainable development.

Specifying terms for the Mountain Green Cover Index are mentioned in the SDG metadata for indicator 15.4.2 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-04-02.pdf) and terms for Coverage by protected areas in the SDG metadata for indicator 15.4.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-04-01.pdf).

`fells` are combined with Lapland because independently they brought a lot of noise (*fell* has many other meanings). Initially they were also combined with Scotland, but due to many irrelevant results, Scotland was left out. 

The phrases return some articles which mention `mountain` in a name of a species (e.g. Mountain hare, Mountain zebra, Mountain tapir). Some of these articles might not be about mountains, but identifying and excluding them without losing relevant articles would be quite challenging.

This query consists of 2 phrases. Terrestrial and freshwater terms are **not** combined with the phrases 15.4.

#### Phrase 1

This phrase aims to find research about conserving and improving conservation of mountain ecosystems and their biodiversity. It includes research about establishing/managing protected areas, key biodiversity areas and vegetation covered areas of the mountains (Mountain Green Cover Index). Specifying terms for areas counted as green cover for the Mountain Green Cover Index `forest` `shrubs` `trees` `pasture` `cropland` `grassland` `wetland` are mentioned in the SDG metadata for indicator 15.4.2 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-04-02.pdf). `KBA` is not freely truncated due to noise from "kbar" (a unit).

The elements of this phrase are *(conserving OR action + management/conservation/protected areas/instruments) + ecosystem/biodiversity + mountains*

```py
TS=
(
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
          NEAR/5
              ("management" OR "conservation" OR "protection" OR "restoration" OR "sustainable"
              OR "Protected area$" OR "Wilderness area$" OR "Nature reserve$" OR "National park$"
              OR "Natural monument$" OR "Natural feature$"
              OR "Habitat management area$" OR "Species management area$"
              OR "Protected landscape$"
              OR "key biodiversity area$" OR "KBA" OR "KBAs"
              OR "important sites for biodiversity"
              OR "Mountain Partnership"
              OR "Mountain Green Cover Index"
              OR "Convention on Biological Diversity" OR "CBD"
              OR "Convention on International Trade in Endangered Species of Wild Fauna and Flora" OR "CITES"
              )
        )
      )
      NEAR/15
            ("ecosystem$" OR "habitat$"
            OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
            OR (("diversity" OR "communit*") NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
            OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
            OR (("covered" OR "cover*") NEAR/5 ("green" OR "vegetat*" OR "*forest$" OR "shrub$" OR "tree$" OR "pasture$" OR "cropland$" OR "grassland$" OR "wetland$"))
            )
  )
AND ("mountain*" OR "alpine" OR "highland$" OR ("fell$" NEAR/5 "Lapland"))
)
```

#### Phrase 2

This phrase aims to find research about promoting sustainable use of the services/benefits provided by the mountain ecosystems. The elements of this phrase are *action + sustainable use + ecosystem services + mountains*

```py
TS=
(
  (
    (
      ("promot*" OR "enable" OR "increase" OR "establish" OR "implement*" OR "assure")
      NEAR/5
          (
            ("sustainabl*" OR "environmental*" OR "ecological*")
            NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning")
          )
    )
    NEAR/15
        ("ecosystem$" OR "habitat$"
        OR ("communit*" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
        OR ("diversity" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
        )
  )
  AND ("mountain*" OR "alpine" OR "highland$" OR ("fell$" NEAR/5 "Lapland"))
)
```

### Target 15.5

> **15.5 Take urgent and significant action to reduce the degradation of natural habitats, halt the loss of biodiversity and, by 2020, protect and prevent the extinction of threatened species**
>
> 15.5.1 Red List Index

This target is interpreted to cover research about resisting the degradation of terrestrial and freshwater habitats and their biodiversity, and about restoring and protecting them. It also covers research about protecting threatened species as a part of that.

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
TS=("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
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
              OR (("diversity" OR "species") NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
              )
        )
)
AND
TS=("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
```

#### Phrase 3

This phrase aims to find research about promoting biodiversity and research about protecting threatened species.

The concept of *threatened species* is interpreted according to the classification of the SDG metadata for indicator 15.5.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-05-01.pdf): 
> "Threatened species are those listed on The IUCN Red List of Threatened Species in the categories Vulnerable, Endangered, or Critically Endangered (i.e., species that are facing a high, very high, or extremely high risk of extinction in the wild in the medium-term future)."

The elements of the phrase are *protecting / action + conservation/key biodiversity areas + biodiversity/threatened species*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. Terms about human microbiome and terms which are related to diseases were added to `double NOT` string in order to exclude articles about those. The medical terms were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

```py
TS=
(
  ("manage" OR "conserve" OR "protect" OR "restore" OR "promote"
  OR
    (
      ("promot*" OR "restor*" OR "rehabilita*" OR "support*" OR "ensur*" OR "prioriti$e"
      OR "improv*" OR "enhanc*" OR "strengthen*" OR "increas*"
      OR "maintain*"
      OR "establish*" OR "propose*" OR "proposal$" OR "implement*"
      OR "plans" OR "plan" OR "planned" OR "planning" OR "policy" OR "policies" OR "initiativ*" OR "framework" OR "strategy" OR "governance"
      OR "increas*" OR "strengthen" OR "improv*" OR "enhance" OR "facilitat*"
      )
      NEAR/5
          ("management" OR "conservation" OR "protection" OR "restoration"
          OR "key biodiversity area$" OR "KBA$"
          OR "important sites for biodiversity"
          )
    )
  )
  NEAR/5
      ("biodiversity" OR "biological diversity"
      OR ("diversity" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      OR (("threatened" OR "near extinct*" OR "at risk" OR "endanger*" OR "vulnerable" OR "protected" OR "red list*") NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$"))
      OR "Red List Index"
      OR "RLI" OR "Red List" OR "IUCN" OR "International Union for Conservation of Nature"
      )
)
NOT TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
    NEAR/5
        ("extinction" OR "loss" OR "going extinct")
  )
  NEAR/15
        (
          ("threatened" OR "near extinct*" OR "at risk" OR "endanger*" OR "vulnerable" OR "protected" OR "red list*")
          NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$")
        )
)
NOT TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.6

> **15.6 Promote fair and equitable sharing of the benefits arising from the utilization of genetic resources and promote appropriate access to such resources, as internationally agreed**
>
> 15.6.1 Number of countries that have adopted legislative, administrative and policy frameworks to ensure fair and equitable sharing of benefits

This target is interpreted to cover research about promoting the sharing of benefits arising from genetic resources of terrestrial and freshwater organisms, as well as improving access to these resources. Benefits are defined according to the CBD factsheet on Access and Benefit-Sharing (ABS) (<a id="abs">[CBD, n.d.](#f10)</a>). They range from basic research to development of products. By the definition of the CBD, benefit sharing applies also to benefits arising from the use of traditional knowledge of indigenous and local communities associated with genetic resources.

*The Nagoya Protocol on Access to Genetic Resources and the Fair and Equitable Sharing of Benefits Arising from their Utilization to the Convention on Biological Diversity* is an essential agreement related to this target. CBD webpages on Nagoya protocol (<a id="nagoya">[CBD, Aug 2022](#f9)</a>) were used to define the aims and scope of this target.

In addition to papers about the use of terrestrial and freshwater resources, this query also returns some agricultural papers. They are not excluded from the results since the indicator 15.6.1 includes "Countries that are contracting Parties to the International Treaty on Plant Genetic Resources for Food and Agriculture (PGRFA)" (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-06-01.pdf).

This query consists of 3 phrases. The phrases are limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

This phrase aims to find research about promoting the sharing of genetic resources, including traditional knowledge of the indigenous and local communities. The elements of the phrase are *action + sharing/access + resources/knowledge*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    (
      ("promot*" OR "improv*" OR "enhanc*" OR "strengthen*"
      OR "increas*" OR "expand*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
      )
      NEAR/5 ("share$" OR "sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$" OR "ownership")
    )
    NEAR/15
        ("genetic resource$" OR "gene resources"
        OR ("knowledge" NEAR/3 ("traditional" OR "indigenous" OR "autochthonous" OR "local"))
        )
  )
  AND ("ecosystem$" OR "biotope$" OR "biodiversity" OR "species" OR "plant*" OR "animal$" OR "organism$" OR ("genetic resource$" NOT "human"))
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research about promoting the sharing of benefits derived from utilizing genetic resources, including traditional knowledge of the indigenous and local communities. The elements of the phrase are *action + sharing/access + resources/knowledge + use + benefits*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

While testing the phrase, it was noticed that `knowledge` combined with `local` or `traditional` brings some irrelevant results about various fields (transport, business, education).

```py
TS=
(
  (
    ("promot*" OR "improv*" OR "enhanc*" OR "strengthen*"
    OR "increas*" OR "expand*" OR "stimulat*" OR "encourag*" OR "secure" OR "securing"
    )
    NEAR/5 ("share$" OR "sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$" OR "ownership")
  )
  AND
    (
      (
          ("genetic resource$" OR "gene resource$"
          OR ("knowledge" NEAR/3 ("traditional" OR "indigenous" OR "autochthonous" OR "local"))
          )
          NEAR/5 ("use$" OR "using" OR "utiliz*" OR "utilis*")
      )
      AND
          ("benefit$"
          OR ("results" NEAR/3 ("research" OR "development"))
          OR ("transfer*" NEAR/3 "technolog*")
          OR ("participat*" NEAR/3 "research activit*")
          OR ("develop*" NEAR/3 "product$")
          OR (("monetary" OR "royalties") NEAR/3 ("benefit$" OR "compensat*"))
          OR "bioprospect*"
          )
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.7

> **15.7 Take urgent action to end poaching and trafficking of protected species of flora and fauna and address both demand and supply of illegal wildlife products**
>
> 15.7.1 Proportion of traded wildlife that was poached or illicitly trafficked

This target is interpreted to cover research about stopping poaching and trafficking of protected terrestrial and freshwater species. The target also covers research about the markets or trade for illegal wildlife products. It is somewhat unclear to us whether the target aims to cover all poaching or just poaching of protected species. In the phrases, we have limited poaching to protected/endangered species.

Some particularly susceptible species were added to the phrase for better recall. The source for these was The UN's World Wildlife Crime Report (<a id="wwc">[UNODC, 2020](#f13)</a>).

This query consists of 3 phrases. The phrases are limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

This phrase aims to find research about ending poaching and trafficking of protected species.

While testing the phrase it was noticed that the combination of `trafficking` and `animal` returns some irrelevant results about animal physiology (receptor trafficking, etc.). These are hard to exclude without losing relevant results.

The elements of the phrase are *action + poaching/trafficking + protected species*. It is limited by the exclusion of marine habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
    OR "prevent*" OR "combat*" OR "resist*" OR "tackle*"  
    OR "reduc*" OR "decreas*" OR "minimi*" OR "control*"
    )
    NEAR/5
        ("poach*" OR "trafficking" OR "trafficked" OR "smuggl*")
  )
  NEAR/15
      (
        ("protect*" OR "endanger*" OR "threat*" OR "extinct*" OR "vulnerable")
        NEAR/5 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$")
       
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research about the markets/trade for illegal wildlife products. No action terms are combined with the markets (reduced demand & supply) because the phrase finds so few works if limited by action terms.

The elements of the phrase are *protected species + illegal products + markets*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

```py
TS=
(
  (
    (
      ("protected" OR "endanger*" OR "threatened*" OR "extinct*" OR "vulnerable")   
      NEAR/5 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$")
    )
    NEAR/15
        (
          ("illegal*" OR "illicit*" OR "criminal" OR "crime")
          NEAR/5
              ("product$" OR "manufact*" OR "merchandise$" OR "artifact*" OR "fabricat*" OR "handicraft$" OR "handiwork$"
              OR "market$*" OR "supply" OR "supplier$" OR "supplied" OR "demand" OR "trade" OR "trading" OR "purchas*"
              )
        )
  )
  AND ("market$*" OR "supply" OR "supplier$" OR "supplied" OR "demand" OR "trade" OR "trading" OR "purchas*" OR "livlihood$")
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 3

This phrase aims to find research about protected/endangered species mentioning *The Convention on International Trade in Endangered Species of Wild Fauna and Flora (CITES)*. The elements of the phrase are *protected species + CITES*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

Action terms are not combined with this phrase since it could be assumed that articles mentioning protected/endangered species and CITES are action-oriented. Still, the phrase is quite broad and return also some articles which are more about target 15.5 (protection of threatened species) than about the trade on them. 

The term `CITES` is combined to a string of species terms in order to exclude irrelevant articles which use cite as a verb. Even still, some such articles are retrived by this phrase.

```py
TS=
(
  (
    ("protect*" OR "endanger*" OR "threat*" OR "extinct*" OR "vulnerable")
    NEAR/5 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$")
  )
  AND 
    ("Convention on International Trade in Endangered Species of Wild Fauna and Flora" 
    OR ("CITES" NEAR/15 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"))
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
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
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.9

> **15.9 By 2020, integrate ecosystem and biodiversity values into national and local planning, development processes, poverty reduction strategies and accounts**
>
> 15.9.1 (a) Number of countries that have established national targets in accordance with or similar to Aichi Biodiversity Target 2 of the
> Strategic Plan for Biodiversity 2011–2020 in their national biodiversity strategy and action plans and the progress reported towards these targets;
> and (b) integration of biodiversity into national accounting and reporting systems, defined as implementation of the System of Environmental-Economic Accountings

This target is interpreted to cover research about national or local strategies/accounting/reporting and ecosystem values, conserving biodiversity, or the CBD Aichi Biodiversity Target 2 (CBD webpages; <a id="aichi">[CBD, Sep 2020](#f12)</a>). This covers research about national plans in context of *Aichi biodiversity targets* and *System of Environmental-Economic Accounting* which are mentioned in the SDG metadata for indicator 15.9.1 (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-09-01.pdf). Biodiversity and ecosystem values are interpreted to be about protecting and conserving biodiversity and ecosystems. Even though the target specifies development processes and poverty reduction, `strategies` and `plans` in the phrases are not limited to just these. 

Articles about ecosystem and biodiversity values in national planning were assumed to be related to promoting the implementation of these. Hence, no action terms (such as promote/enable/etc.) were combined with the phrase of this target. 

This query consists of 1 phrase. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

The elements of this phrase are *(Aichi/biodiversity values / conservation + ecosystem/biodiversity) + national targets/strategies*. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results, e.g. `public health` `epidemiology` `national health` `healthcare` `health effects` `archaeology` `architecture*`. A set of medical terms about human microbiome and diseases was also added to exclude noise found in some cases when `diversity` is combined with `biological` etc. These were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

While testing the phrase it was noticed that the term `environment` will bring a lot noise due to its use on various fields (business environment, cultural environment, learning environment, etc.). To exclude these, `environment` was combined with a string of species & habitat terms.

```py
TS=
(
  ("Aichi Biodiversity Target$" OR "Strategic Plan for Biodiversity" OR "ecosystem value$" OR "biodiversity value$"
  OR
    (
      ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving"
      OR "improv*" OR "restor*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "support"
      )
      NEAR/5
          ("ecosystem$" OR "habitat$" OR "biotope$"
          OR (("communit*"  OR "environment*") NEAR/5 ("ecolog*" OR "biological" OR "biodiversity" OR "species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "forest$" OR "woodland$" OR "taiga" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR "tundra" OR "freshwater" OR "limnic" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
          )
    )
  OR
    (
      ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving"
      OR "promoting" OR "promote" OR "improv*" OR "increase"
      OR "restor*" OR "enhanc*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "support"
      OR "System of Environmental-Economic Accounting" OR "SEEA"
      )
      NEAR/5
          ("biodiversity" OR "biological diversity"
          OR ("diversity" NEAR/5 ("ecolog*" OR "biological" OR "species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "forest$" OR "woodland$" OR "taiga" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR "tundra" OR "freshwater" OR "limnic" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
          )
    )
  )
  AND
      ("National Biodiversity Strategy and Action Plan"
      OR ("NBSAP" NEAR/5 ("Convention on Biological Diversity" OR "CBD"))
      OR
        (
          ("national" OR "local" OR "government*" OR "regional" OR "sectoral" OR "municipal" OR "federal" OR "poverty reduction" OR "reduc* poverty" OR "anti poverty" OR "antipoverty")
          NEAR/5
              ("target$" OR "goal$" OR "program*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "governance"
              OR "plan" OR "planning" OR "plans" OR "action plan$" OR "development" OR "developing"
              OR "accounting" OR "reporting"
              )
        )
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.a

> **15.a Mobilize and significantly increase financial resources from all sources to conserve and sustainably use biodiversity and ecosystems**
>
> 15.a.1 (a) Official development assistance on conservation and sustainable use of biodiversity; and (b) revenue generated and finance mobilized from biodiversity-relevant economic instruments

This target is interpreted to cover research about financing the conservation and sustainable use of biodiversity and ecosystems. Financial resources include development assistance and finance mobilized from economic instruments, including incentives mentioned in the SDG metadata for indicator 15.a.1  (<a id="SDGmetarep">[UN Statistics Division 2022](#f3)</a>; https://unstats.un.org/sdgs/metadata/files/Metadata-15-0a-01.pdf) and financial instruments or capacity building initiatives mentioned in the HLPF Background note for SDG 15 (<a>[UN-DESA/DSDG et al. 2018](#f4)</a>).

We assume that all research about financial resources for conserving and sustainable use of biodiversity and ecosystem is relatively action-oriented. Hence, no additional action terms (such as increase, enhance, etc.) were combined with this query.

This query consists of 1 phrase. It is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

The elements of this phrase are *protection/sustainable use + ecosystem/biodiversity + financing/instruments*. The phrase is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results. A set of medical terms about human microbiome and diseases was also added to exclude noise found in some cases when `diversity` is combined with `species` etc. These were picked from a set of irrelevant papers found when testing the phrases and are not chosen systematically. It is possible that terms like `parasite` `infection` or `immunology` will exclude also relevant results.

As the use of term `ecosystem` by others than natural sciences brings irrelevant results, it was combined with a string of species and habitat terms. Terms `community` `area` and `zone` were left out from the phrase in order to exclude irrelevant results.

```py
TS=
(
  (
    ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving"
    OR "promoting" OR "promote" OR "improv*" OR "restor*" OR "enhanc*" OR "strengthen*" OR "maintain*" OR "preserv*" OR "support"
    OR
      (
        ("sustainabl*" OR "responsibl*" OR "environmental*" OR "ecological*")
        NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning")
      )
    )
    NEAR/15
        (
          ("ecosystem$" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "peatland$" OR "bog$" 		OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
          ) 
        OR "habitat$" OR "biotope$"
        OR "biodiversity" OR "biological diversity"
        OR ("diversity" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$"))
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
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

### Target 15.b

> **15.b Mobilize significant resources from all sources and at all levels to finance sustainable forest management and provide adequate incentives to developing countries to advance such management, including for conservation and reforestation**
>
> 15.b.1 (a) Official development assistance on conservation and sustainable use of biodiversity; and (b) revenue generated and finance mobilized from biodiversity-relevant economic instruments

This target is interpreted to cover research about increasing financing and sustainable forest management. It also covers research about increasing incentives to developing countries for advancing sustainable forest management, conservation of forests and reforestation.

This query consists of 2 phrases. Terrestrial and freshwater terms are **not** combined with the phrases 15.b.

#### Phrase 1

This phrase aims to find research about financing and incentives for promotion of sustainable forest management. Part of the phrase (aiming for advancing sustainable forest management) is similar to the 15.2 phrase 1, but the specified management practises are left out of the phrase to exclude results which might be less about sustainability and more about forestry as a business.

The elements of the phrase are *action + financing/incentives/instruments + sustainable use/practises/strategies/goals + forests*.

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
          OR "incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
          OR "ODA" OR "cooperation fund$" OR "development spending"
          OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance"))
          )
  )
  AND
    (
      (
        ("sustainabl*" OR "responsibl*" OR "environmental*" OR "ecological*")
        NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning")
      )
    OR
      (
        ("sustainabl*" OR "responsibl*" OR "environmental*" OR "ecological*")
        NEAR/15
            ("practice$" OR "method$" OR "forestry operation$"
            OR "policy" OR "policies"
            OR "Forest area change"
            OR "Above-ground biomass in forest"
            OR ("Proportion" NEAR/3 "protected areas")
            OR ("Proportion" NEAR/3 "long-term management plan")
            OR "Forest under certification"
            OR "Certified forest area"
            )
      )
    OR ("protected" NEAR/3 "forest*")
    OR ("reserved" NEAR/3 "forest*")
    OR "UN Strategic Plan for Forests" OR "UNSPF"
    OR "Global Forest Goals" OR "GFG$"
    )
  AND 
    ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
)
```

#### Phrase 2

This phrase aims to find research about promoting incentives to developing countries for reforestation and conservation of forests. The elements of the phrase are *action + financing/incentives/instruments + reforestation/conservation + forests + developing countries*.

Terms `planting trees` and `tree plantations` are added to this string, but not used in the strings of target 15.2. In the context of this phrase these terms are likely to return relevant results. Whereas in the strings of 15.2 without the connection to incentives, they might bring noise.

Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (<a id="UNLDCs">[United Nations, 2016, 2017, 2018, 2019, 2020, 2021](#f2)</a>). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters).

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
          OR "incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
          OR "ODA" OR "cooperation fund$" OR "development spending"
          OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance"))
          )
  )
  AND
  (
    ("afforestr*" OR "reforestr*"
    OR
      (
        ("increas*" OR "expand*")
        NEAR/5
          ("woodland$" OR "silvicultur*" OR "arboricultur*"
          OR ("*forest*" NEAR/3 ("cover*" OR "area$" OR "zone$" OR "*land$"))
          )
      )
    OR
      (
        ("restor*" OR "rehabilita*" OR "conservation" OR "protect*" OR "maintain*" OR "preserv*" ) 
        NEAR/5 ("*forest*" OR "woodland$")
      )
    OR "UN-REDD" OR "UN REDD" OR "United Nations REDD" 
	  OR (("planting" OR "plant" OR "plantation") NEAR/3 "tree$")
    )
  )
  AND ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
  AND
    ("least developed countr*" OR "least developed nation$"
    OR "developing countr*" OR "developing nation$" OR "developing states" OR "developing world"
    OR "less developed countr*" OR "less developed nation$" OR "under developed countr*" OR "under developed nation$" OR "underdeveloped countr*" OR "underdeveloped nation$" OR "underserved countr*" OR "underserved nation$" OR "deprived countr*" OR "deprived nation$"
    OR "middle income countr*" OR "middle income nation$"
    OR "low income countr*" OR "low income nation$" OR "lower income countr*" OR "lower income nation$"
    OR "poor countr*" OR "poor nation$" OR "poorer countr*" OR "poorer nation$"
    OR "lmic" OR "lmics" OR "third world" OR "global south" OR "lami countr*" OR "transitional countr*" OR "emerging economies" OR "emerging nation$"
    OR  "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"      OR  "Antigua and Barbuda" OR "Antigua & Barbuda" OR "antiguan$" OR "Bahamas" OR "Bahrain" OR "Barbados" OR "Belize" OR "Cabo Verde" OR "Cape Verde" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Cuba" OR "cuban$" OR "Dominica*" OR "Dominican Republic" OR "Micronesia*" OR "Fiji" OR "fijian$" OR "Grenada*" OR "Guinea-Bissau" OR "Guyana*" OR "Haiti*" OR "Jamaica*" OR "Kiribati*" OR "Maldives" OR "maldivian$" OR "Marshall Islands" OR "Mauritius" OR "mauritian$" OR "Nauru*" OR "Palau*" OR "Papua New Guinea*" OR "Saint Kitts and Nevis" OR "st kitts and nevis" OR "Saint Lucia*" OR "St Lucia*" OR "Vincent and the Grenadines" OR "Vincent & the Grenadines" OR "Samoa*" OR "Sao Tome" OR "Seychelles" OR "seychellois*" OR "Singapore*" OR "Solomon Islands" OR "Surinam*" OR "Timor-Leste" OR "timorese" OR "Tonga*" OR "Trinidad and Tobago" OR "Trinidad & Tobago" OR "trinidadian$" OR "tobagonian$" OR "Tuvalu*" OR "Vanuatu*" OR "Anguilla*" OR "Aruba*" OR "Bermuda*" OR "Cayman Islands" OR "Northern Mariana$" OR "Cook Islands" OR "Curacao" OR "French Polynesia*" OR "Guadeloupe*" OR "Guam" OR "Martinique" OR "Montserrat" OR "New Caledonia*" OR "Niue" OR "Puerto Rico" OR "puerto rican" OR "Sint Maarten" OR "Turks and Caicos" OR "Turks & Caicos" OR "Virgin Islands"      OR  "Afghanistan" OR "afghan*" OR "Armenia*" OR "Azerbaijan*" OR "Bhutan" OR "bhutanese" OR "Bolivia*" OR "Botswana*" OR "Burkina Faso" OR "Burundi" OR "Central African Republic" OR "Chad" OR "Eswatini" OR "eswantian" OR "Ethiopia*" OR "Kazakhstan*" OR "kazakh" OR "Kyrgyzstan" OR "Kyrgyz*" OR "kirghizia" OR "kirgizstan" OR "Lao People’s Democratic Republic" OR "Laos" OR "Lesotho" OR "Malawi" OR "malawian" OR "Mali" OR "Mongolia*" OR "Nepal*" OR "Niger" OR "North Macedonia" OR "Republic of Macedonia" OR "Paraguay" OR "Moldova*" OR "Rwanda$" OR "South Sudan" OR "sudanese" OR "Swaziland" OR "Tajikistan" OR "tadjikistan" OR "tajikistani$" OR "Turkmenistan" OR "Uganda*" OR "Uzbekistan" OR "uzbekistani$" OR "Zambia" OR "zambian$" OR "Zimbabwe*"      OR   "albania*" OR "algeria*" OR "angola*" OR "argentina*" OR "azerbaijan*" OR "bahrain*" OR "belarus*" OR "byelarus*" OR "belorussia" OR "belize*" OR "honduras" OR "honduran" OR "dahomey" OR "bosnia*" OR "herzegovina*" OR "botswana*" OR "bechuanaland" OR "brazil*" OR "brasil*" OR "bulgaria*" OR "upper volta" OR "kampuchea" OR "khmer republic" OR "cameroon*" OR "cameroun" OR "ubangi shari" OR "chile*" OR "china" OR "chinese" OR "colombia*" OR "costa rica*" OR "cote d’ivoire" OR "cote divoire" OR "cote d ivoire" OR "ivory coast" OR "croatia*" OR "cyprus" OR "cypriot" OR "czech" OR "ecuador*" OR "egypt*" OR "united arab republic" OR "el salvador*" OR "estonia*" OR "eswatini" OR "swaziland" OR "swazi" OR "gabon" OR "gabonese" OR "gabonaise" OR "gambia*" OR "ghana*" OR "gibralta*" OR "greece" OR "greek" OR "honduras" OR "honduran$" OR "hungary" OR "hungarian$" OR "india" OR "indian$" OR "indonesia*" OR "iran" OR "iranian$" OR "iraq" OR "iraqi$" OR "isle of man" OR "jordan" OR "jordanian$" OR "kenya*" OR "korea*" OR "kosovo" OR "kosovan$" OR "latvia*" OR "lebanon" OR "lebanese" OR "libya*" OR "lithuania*" OR "macau" OR "macao" OR "macanese" OR "malagasy" OR "malaysia*" OR "malay federation" OR "malaya federation" OR "malta" OR "maltese" OR "mauritania" OR "mauritanian$" OR "mexico" OR "mexican$" OR "montenegr*" OR "morocco" OR "moroccan$" OR "namibia*" OR "netherlands antilles" OR "nicaragua*" OR "nigeria*" OR "oman" OR "omani$" OR "muscat" OR "pakistan*" OR "panama*" OR "papua new guinea*" OR "peru" OR "peruvian$" OR "philippine$" OR "philipine$" OR "phillipine$" OR "phillippine$" OR "filipino$" OR "filipina$" OR "poland" OR "polish" OR "portugal" OR "portugese" OR "romania*" OR "russia" OR "russian$" OR "polynesia*" OR "saudi arabia*" OR "serbia*" OR "slovakia*" OR "slovak republic" OR "slovenia*" OR "melanesia*" OR "south africa*" OR "sri lanka*" OR "dutch guiana" OR "netherlands guiana" OR "syria" OR "syrian$" OR "thailand" OR "thai" OR "tunisia*" OR "ukraine" OR "ukrainian$" OR "uruguay*" OR "venezuela*" OR "vietnam*" OR "west bank" OR "gaza" OR "palestine" OR "palestinian$" OR "yugoslavia*" OR "turkish"  OR "turkey" OR "georgia"
    )
)
```

### Target 15.c

> **15.c Enhance global support for efforts to combat poaching and trafficking of protected species, including by increasing the capacity of local communities to pursue sustainable livelihood opportunities**
>
> 15.c.1 Proportion of traded wildlife that was poached or illicitly trafficked

This target is interpreted to cover research about combatting poaching and trafficking of protected species, including research about capacity and poaching (e.g. education, collaboration). It also covers research about poaching of protected animals in relation to the local communities' opportunities for sustainable livelihood. It is somewhat unclear to us whether the target aims to cover all poaching or just poaching of protected species. In the phrases, we have limited poaching to protected/endangered species.

This interpretation is the same as the topic approach, and the strings are currently identical. This may need to be revisited, for example, should the topic approach cover all research about poaching?

Some particularly susceptible species were added to the phrases for better recall. The source for these was The UN's World Wildlife Crime Report (<a id="wwc">[UNODC, 2020](#f13)</a>).

This query consists of 2 phrases. Both phrases are limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

#### Phrase 1

The elements of the phrase are *action/capacity building/instruments + poaching/trafficking + protected species*. The phrase is limited by the exclusion of `marine` habitats (except when a **terrestrial or freshwater term** is mentioned) and some other terms which were detected to bring irrelevant results.

This phrase is similar to target 15.7 phrase 1, but is focused on finding research about the support and capacity building (including financing) to fight against poaching and trafficking of protected species. As in target 15.7, the combination of `trafficking` and `animal` return some irrelevant results about animal physiology (receptor trafficking, etc.). These are hard to exclude without losing relevant results.

```py
TS=
(
  (
    ("stop*" OR "end" OR "ends" OR "ended" OR "ending" OR "halt*"
    OR "resist*" OR "reduc*" OR "decreas*" OR "minimi*" OR "tackle*" OR "control*" OR "prevent*" OR "combat*"
    OR "anti-poaching"
    OR "capacity building" OR "capacity development" OR "capacity"
    OR "cooperation" OR "collaboration" OR "network$" OR "support"
    OR "policy" OR "policies" OR "empower*"
    OR "knowledge transfer*"
    OR (("raise" OR "raising") NEAR/3 ("awareness" OR "knowledge"))
    OR ("disseminat*" NEAR/3 "information")
    OR "educat*"
    OR "Convention on International Trade in Endangered Species of Wild Fauna and Flora" OR "CITES"
    OR "Landscapes for People, Food and Nature partnership"
    )
    NEAR/15 ("poach*" OR "trafficking" OR "trafficked" OR "smuggl*" OR "illegal harvest*")
  )
  AND
    (
      ("protect*" OR "endanger*" OR "threat*" OR "extinct*" OR "vulnerable")
      NEAR/5
          ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "mammals$"
          OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"
          )
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

#### Phrase 2

This phrase aims to find research about poaching and trafficking of protected species in relation to sustainable livelihood opportunities of the local communities. `CITES` is added as an alternative to poaching or trafficking of protected species because often the implications to the local communities follow from the application of CITES decisions (<a id="cites">[CITES & General Secretariat of the Organization of American States, 2015](#f14)</a>).

The elements of the phrase are *CITES/poaching/trafficking + protected species + livelihood of local communities*. In order to specify to the terrestrial and freshwater species, the phrase is combined with **Terrestrial and freshwater terms** with `AND`.

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
        (
          ("protect*" OR "endanger*" OR "threat*" OR "extinct*" OR "vulnerable")
          NEAR/5
              ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "mammals$"
              OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$"
              )
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
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "decision forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$" OR "archaeolog*" OR "architect*") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```

## 5. Contributions

* v1.0.0: Leena Byholm (Dec 2021-Sep 2022)

* Internal review: Caroline S. Armitage (May 2022)

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
