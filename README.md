# Information about these files

These files contain search strings to find publications related to certain [Sustainable development goals](https://sdgs.un.org/goals). 

This work is a product of the project *Bærekraftsforskning for alle – en transparent kartleggings- og gjenfinningstjeneste* (Sustainable development research for all – a transparent mapping and discovery tool), a Norwegian project supported by the National Library of Norway. **[Read more about the project and find contact details here](https://www.uib.no/en/ub/148804/sustainable-development-research-all-%E2%80%93-transparent-mapping-and-discovery-tool)**. This project is led by the University of Bergen Library, partnered with the libraries at Western Norway University of Applied Sciences and the University of Stavanger. Natural Resources Institute Finland (Luke) has contributed with search strings for two SDGs as an external collaborator.

File names in this set consist of the SDG and the approach used (topic vs. action), as well as the platform/syntax for the string. The approach relates to decisions about what kind of research the string should find: research closely related to the actions of the SDG targets (*action*), or research more broadly related to the topics in the targets (*topic*). *You can read more about these below*. Stable versions are saved as "releases"; in between releases, there may be changes to the strings. A status message at the top of each file gives information.

## Why are we building strings? How do they differ to existing mappings?

Previous research has shown that mappings of SDG-"related" research do not match up very well ([Armitage, Lorenz & Mikki 2020](https://doi.org/10.1162/qss_a_00071); [Purnell 2022](https://doi.org/10.1162/qss_a_00215)). This is perhaps unsurprising when you consider that there are different ways to interpret what an SDG covers, different viewpoints on which research themes should be counted as "related", different mapping methods, and different data sources (see our previous work, [Armitage, Lorenz & Mikki 2020](https://doi.org/10.1162/qss_a_00071)). For example, should *SDG 3 Good health* cover all medical research? Does *SDG 13 Climate Action* cover basic climate science? You will probably get different answers depending on who you ask.

Instead of trying to find the "right" answer, we think multiple mappings (which can capture different views of relatedness) are a good idea. But in order for these to have meaning, documentation must explain a) what it is supposed to find (i.e. how the SDG was interpreted and what research is considered relevant), and b) how the mapping is done. We have written our own strings because we believe there is currently a gap for this kind of mapping. In short:

- Our strings allow mapping of research to individual SDG targets ("target-level"). This is useful for identifying where a research set is focused within an SDG. They can be combined to examine the whole SDGs ("goal-level").
- We provide two types of strings: *action* and *topic* approaches, which have different interpretations of "relevance".
- The strings are manually curated. They map at the publication-level (rather than journal or subject cluster), using traditional search methods (e.g. matching terms in the titles, abstracts and keywords). The benefit of this is that it is easier to understand why a result is in or out, the drawback that we sacrifice potential additional recall provided by machine learning.
- For each string and target, we document :
  - How we have interpreted which research themes should be considered "relevant" to each SDG target
  - Sources we have used to identify search terms and/or define terminology
  - Choices we have made regarding inclusion/exclusion, interpretations or syntax (e.g. truncation)

For more thoughts about mappings, see also [Rafols, Noyons, Confraria & Ciarli (2021)](https://doi.org/10.31235/osf.io/yfqbd)

## Which SDGs, platforms and languages are covered? 

Currently, we are working on ten of the SDGs: SDGs 1, 2, 3, 4, 7, 11, 12, 13, 14 and 15. The project group is responsible for eight of these; an external collaborator from Natural Resources Institute Finland for the other two. If you like our method and could consider contributing, you are welcome to get in touch.

The strings available at this time (Oct 2022) are formatted in Web of Science syntax (and can be run against the Web of Science Core collection from Clarivate); these have "WoS" at the end of the file name. These are in English. While these strings are built for the WoS platform, this work is not affiliated with Web of Science/Clarivate.

We are currently working on a version in Python which can be run against any list of works in csv format. This version will be in English and Norwegian.

## What kind of results should I expect when using these strings?

This depends on which string you use:

**"Action" strings** : The *action approach* aims to find research related to the actions mentioned in the SDG targets and indicators. 
This is done by looking for works which include a formulation indicating relation to the action, *e.g. "...reducing malnutrition"; "...ensuring rights of small-scale fishers"; "...policies for improving school completion among...".*. These can be verbs, or terms indicating relation to real-world change, such as "policy". 
You might therefore expect to find a "core" set of SDG-related research, directly mentioning actions in the SDG targets. This set is likely to be a **smaller** than when using methods which identify research via it containing certain topics, being published in certain journals, or mapped to a citation cluster (depending of course on the individual parameters used).  

**"Topic" strings** : The *topic approach* aims to find research that is related to the topics mentioned in the SDG targets and indicators. 
This is done by looking for works which mention the topic, *e.g. "malnutrition"; "school completion"; "rights of small-scale fishers"*.
You can therefore expect to find a **larger** set of research than when using the *action approach* (baseline testing indicates that result sets from the *topic approach* are 3-5x larger than when using the *action approach*, depending on SDG). However, the results set you find using the *topic approach* may still be smaller than you would find in other mappings which use a very wide interpretation of relatedness (for example, an even larger set would be found if you considered all medical research as relevant for SDG3, as opposed to the topics mentioned in the targets). 

We have tried to be consistent in the approaches, but there are occasional exceptions in the way that we apply these approaches at the string-level, as we are reliant on language. Some terms are ambiguous and thus difficult to apply a hard set of rules to. For example, terms such as "energy" could be to do with energy technology, or with astrophysics, or biology, or medicine; thus the string construction must be adapted to avoid excessive noise. Please see the documentation on the individual files. 

An early description of these approaches can be found in [Armitage, Lorenz & Mikki (2020)](https://doi.org/10.1162/qss_a_00071). 

## Current status and planned changes?
We have finished a version 1 that can be used for nine of the SDGs (Web of Science syntax) (see "Releases"). SDG 12 will be added later. We consider this a "version": We think the strings are functioning relatively well, but they can likely be improved after testing and feedback, and may require changes over time. We have currently tested the strings in an informal way while building and plan to carry out more formal testing in Q1 2023.  

We are currently working on a topic approach set of strings in Python, which can be run against any list of works in csv format. This will be released in late 2022/early 2023. 

## How do I use these strings? 

Web of Science syntax strings ("WoS" files): Each file contains a search string for a specific SDG, broken up into phrases by target. If you have access to Web of Science Core Collection (hereafter WoS), you can view the total SDG results by clicking the link at the top of each file. If you want to examine individual targets/phrases, the strings are formatted to be copied and pasted into the "advanced search" interface in WoS. You can copy strings using the "copy" icon (two squares) that appears in the top right corner of each code block when holding the mouse over it, and paste it directly into the search box of Web of Science advanced search. You can then combine several phrase searches in the WoS interface by selecting those you have searched for in the history, and combining them with `OR`. The majority of strings use the "topic" field in WoS - title, abstract, author keywords, and Keywords Plus(R) - and thus begin with the code `TS`. In SDG14, the field "journal title" (`SO`) is used also. 

You are welcome to translate the strings into other database syntax or tools, or edit a version to fit your needs. We are interested in hearing about work that comes from these strings, so please consider sharing with us if you have used or adapted them! You are also welcome to contact is with feedback. Our email can be found on the [project homepage](https://www.uib.no/en/ub/148804/sustainable-development-research-all-%E2%80%93-transparent-mapping-and-discovery-tool).

## How should I cite?

Please see the suggested citation in Zenodo for the doi for your version. Suggested citation v1.0.0: Armitage, C. S., Bjerkan, H. M., Byholm, L. P., Gåsemyr, I., Lorenz, M., & Seland, E. H. (2022). Search strings for finding SDG-related research, Bergen-approach (v1.0.0). doi: https://doi.org/10.5281/zenodo.7241690

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7241690.svg)](https://doi.org/10.5281/zenodo.7241690)

## Related works

This work is a continuation of the strings developed for the work [Armitage, Lorenz & Mikki (2020)](https://doi.org/10.1162/qss_a_00071). The release v.2019-12 contains strings for SDGs 1,2,3,7,13 & 14 developed for this work during 2019, and should be the same as those deposited openly on publication (tab format, published May 2020) which can be found in DataverseNO at https://doi.org/10.18710/98CMDR.

## License

Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

These strings are licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
