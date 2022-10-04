# Information about these files - SDGstrings_wos

The files in this repository contain search strings to find publications related to certain [Sustainable development goals](https://sdgs.un.org/goals). This work is a product of the project *Bærekraftsforskning for alle – en transparent kartleggings- og gjenfinningstjeneste* (Sustainable development research for all – a transparent mapping and discovery tool), a Norwegian project supported by the National Library of Norway. **[Read more about the project and find contact details here](https://www.uib.no/en/ub/148804/sustainable-development-research-all-%E2%80%93-transparent-mapping-and-discovery-tool)**.

File names consist of the SDG and the approach used (topic vs. action). The approach relates to decisions about what kind of research the string should find: research closely related to the actions of the SDG targets ("action"), or research more broadly related to the topics in the targets ("topic"). You can read more about these below. **The strings are a work-in-progress, and are at different stages of development - within each file there is a description of its current status at the top.** 

### Which SDGs are covered? 

Currently, we are working on 10 of the 17 SDGs: SDGs 1, 2, 3, 4, 7, 11, 12, 13, 14 and 15. The project group is responsible for 8 of these, while an external collaborator is working on the other two. If you like our method and could consider contributing, you are welcome to get in touch.

### How are these strings different to other mappings?

- These strings allow mapping of research to individual SDG targets ("target-level"). This is useful for identifying where a research set is focused within an SDG. They can be combined to examine the whole SDGs ("goal-level").
- The strings are manually curated. They map at the publication-level (rather than journal or subject cluster), using traditional search methods (e.g. matching terms in the titles, abstracts and keywords).
- For each string, we document :
  - How we have interpreted which research themes should be considered "relevant" to each SDG target
  - Sources we have used to identify search terms and/or define terminology
  - Choices we have made regarding inclusion/exclusion, interpretations or syntax (e.g. truncation)

### What kind of results should I expect when using these strings?

This depends on which version of the strings you use:

**"Action" strings** : The "action" approach aims to find research related to the actions mentioned in the SDG targets and indicators. 
This is done by looking for works which include a formulation indicating relation to the action, *e.g. "...reducing malnutrition"; "...ensuring rights of small-scale fishers"; "...policies for improving school completion among...".*. These can be verbs, or terms indicating relation to real-world change, such as "policy". 
You might therefore expect to find a **smaller** set of research than when using methods which identify research by seeing if it mentions certain topics, is published in certain journals, or is mapped to a citation cluster (depending of course on the individual parameters used).  

**"Topic" strings** : The "topic" approach aims to find research that is related to the topics mentioned in the SDG targets and indicators. 
This is done by looking for works which mention the topic, *e.g. "malnutrition"; "school completion"; "rights of small-scale fishers"*.
You can therefore expect to find a **larger** set of research than the action approach. However, this set may still be smaller than you would find by using a very wide interpretation of relatedness (for example, an even larger set would be found if you considered all medical research as relevant for SDG3, as opposed to the topics mentioned in the targets). 

We have tried to be consistent in the approaches, but there are occasional exceptions in the way that we apply these approaches at the string-level, as we are reliant on language - some terms are ambiguous and thus difficult to apply a hard set of rules to. For example, terms such as "energy" could be to do with energy technology... or could be to do with astrophysics, or biology, or medicine; thus the string construction must be adapted to avoid excessive noise. Please see the documentation on the individual files. 

An early description of these approaches can be found in [Armitage, Lorenz & Mikki (2020)](https://doi.org/10.1162/qss_a_00071). 

### When will the strings be ready to use?
We aim to finish the current version of 9 SDGs within October 2022, when a version will be published on Zenodo. We consider this a "version", rather than a finished product - it will likely be necessary with improvements after testing and over time. SDG 12 will come later in the year. 

### How do I use and cite these strings? 

Each file contains a search string for a specific SDG, broken up into phrases by target. The strings are formatted to be copied and pasted into the "advanced search" interface in the Web of Science Core Collection. You can copy strings using the "copy" icon (two squares) that appears in the top right corner of each code block when holding the mouse over it, and paste it directly into the search box of Web of Science advanced search. You can then combine several phrase searches in the Web of Science interface by selecting those you have searched for in the history, and combining them with `OR`. The majority of strings use the "topic" field in WoS - title, abstract, author keywords, and Keywords Plus(R) - and thus begin with the code `TS`. In SDG14, the field "journal title" (`SO`) is used also. 

You are welcome to translate the strings into other database syntax or tools, or edit a version to fit your needs. We are interested in hearing about work that comes from these strings, so please consider sharing with us if you have used them! Our email is on the project homepage.

When the strings are published in Zenodo, a citation file will be added to the repository. 

### Who has written these strings?

You can find contributor information at the bottom of each file. This lists the main authors, and any specialists who have given input.

This work is a continuation of the strings developed for the work [Armitage, Lorenz & Mikki (2020)](https://doi.org/10.1162/qss_a_00071). The release v.2019-12 contains strings for SDGs 1,2,3,7,13 & 14 developed for this work during 2019, and should be the same as those deposited openly on publication (tab format, published May 2020) which can be found in DataverseNO at https://doi.org/10.18710/98CMDR.

### How have the strings been tested?

We have currently only tested the strings in an informal way while building. We plan to carry out and make available the results of more formal testing in Q1 2023. The orignal versions (v2019.1) were only tested for precision; we plan to test this new version for both precision and recall. 

### License

Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
