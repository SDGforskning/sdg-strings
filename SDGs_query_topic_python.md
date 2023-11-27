# Search queries for all currently covered SDGs - topic approach. English and Norwegian.

This file contains a method for searching for SDG relevant academic works within a dataset based on title (here, `result_title`). For SDG14, journal/series title (`journal`) is also used in the section "Marine terms". The script refers to an additional field, `result_id`, when displaying the results.

It currently covers SDGs 1, 2, 3, 4, 7, 11, 12, 13, 14, and 15. This search is an adaptation of the topic searches for individual SDGs which were originally constructed in search syntax for the database Web of Science (WOS, Clarivate). A full documented version of these WOS searches can be found in Github (https://github.com/SDGforskning/sdg-strings) or Zenodo (https://doi.org/10.5281/zenodo.7241689). We have tried to retain a common structure between the WOS and python versions of the searches by dividing into the same "phrases" (i.e. target 1.4 phrase 2 here corresponds to target 1.4 phrase 2 in the WOS syntax searches, unless otherwise noted). Differences between the WOS and python versions are mainly:
- Adaptation to title search, rather than also being able to search in the abstract and keywords. For this reason, some searches have been simplified/broadened. This does not mean that the searches cannot be run on abstracts/longer texts as well, but the results may be noisier. 
- Additional language search. This file will search for SDG-related works written in both English and Norwegian. The English search terms are always provided first, with the Norwegian translated terms on a new line. By translations, we mean direct translations as well as country-specific terminology. Note that in some cases, adjustments are made to the search to deal with specifically Norwegian isses (for example, large amounts of research on salmon anaemia causing noise in a search for human anaemia); these are commented on. In documentation and notes, "(NO)" signifies it is a Norwegian search term being discussed. Because the Norwegian terms have been optimised to find as much SDG-related research as possible for Norway (e.g. including country-specific terminology), care should be taken if the goal of mapping publications is to compare with other countries - for that purpose, we would suggest using the Web of Science strings or only the English terms in this script. 

The general structure of this file is 
1. Import
2. Country sets - searches to identify results mentioning certain countries, used later in searches where the targets refer to certain groups of countries.
3. Searches, split by SDG and target. Under each target, you will find the target text (English and Norwegian), any general notes, lists of search terms ("termlist_xx"), a search, and a preview of results. Note that occasionally, for efficiency, termlists may be re-used within a target (from an earlier phrase).
4. Code to combine all of the labels created in the above part into two columns: SDG-level results (e.g. whether a result can be related to SDG4) and target-level results (e.g. whether a result can be related to target 4.1).  
5. Cleaning

Documentation included in this file is specific to a) implementation of the search in python, b) adaptation to a title search, or c) Norwegian search terms. For documentation of original English term sources, interpretations of SDG targets, relevance choices, and contributor information, see the documentation within the original Web of Science syntax files at the urls above.

To cite, please see the suggested citation in Zenodo for your version: https://doi.org/10.5281/zenodo.7241689


```python
import pandas as pd
import numpy as np
```

## Import

Use file of all results, already pre-labelled with other methods if applicable. 


```python
#Check data
Data.head(2)
```


```python
Data.info()
```


```python
# Tables expand to show long variables (e.g. abstract)
pd.set_option('display.max_colwidth', 1)
```

## Country sets

This section creates columns (T/F) for results that mention groups/combinations of these groups of countries. These are used later in the searches if a topic should be limited to a group of countries. It is done in this way to reduce search time (searches for long country lists only need to be done once, rather than for each target that needs it).

LDC = least-developed countries; SIDS = small-island developing states; LDS = landlocked developing states; LMICs = Low- and middle-income countries. Our classification of countries as least developed countries (LDCs), small island developing states (SIDS) and landlocked developing states (LDS) is taken from the Statistical Annex of United Nations World Economic Situation and Prospects (tables F, H and I) (United Nations, 2016, 2017, 2018, 2019, 2020, 2021). Additional terms for these countries, generic terms for country groups, and terms for low and middle income countries (LMICs) were gathered from the LMIC 2020 filter from the Norwegian Satellite of Cochrane Effective Practice and Organisation of Care (EPOC), developed by the Norwegian Institute of Public Heath (https://epoc.cochrane.org/lmic-filters). Translations to Norwegian were done by the project group. 


```python
LDC_termlist = [
  "least developed countr", "least developed nation", 
  "Angola", "Benin", "beninese", "Burkina Faso", "Burkina fasso", "burkin", "Burundi", "Central African Republic", "central african", "Chad", "Comoros", "comoro islands", 
  "iles comores", "Congo", "Djibouti", "Eritrea", "Ethiopia", "Gambia", "Guinea", "Guinea-Bissau", "guinean", "Lesotho", "lesothan", "Liberia", 
  "Madagasca", "Malawi", "Mauritania", "Mozambique", "mozambican", "Niger", "Rwanda", "Sao Tome and Principe", "Senegal", "Sierra Leone", 
  "Somalia", "South Sudan", "Sudan", "sudanese", "Togo", "togolese", "tongan", "Uganda", "Tanzania", "Zambia", "Cambodia", "Kiribati", 
  "Lao People’s democratic republic", "Laos", "Myanmar", "myanma", "Solomon islands", "Timor Leste", "Tuvalu", "Vanuatu", 
  "Afghanistan", "afghan", "Bangladesh", "Bhutan", "Nepal", "Yemen", "Haiti", 

  "minst utviklede land", "lavinntektsland", "låginntektsland",
  "eritreisk", "eritreer","eritrear", "gambisk", "gambier", "Den Sentralafrikanske republikk", "sentralafrikan", "Tsjad", "Komor", "Kongo", "Etiopi", "bissauguinean", "lesothi", "liberisk", "Madagas", "gasser", "mauritanier", "mauritaniar", "mauritanisk", "Mosambik", "Sao Tome og Principe", "saotomes", "Sør-Sudan", "sørsudan", 
  "Kambodsja", "Salomonøyene", "salomon", "Øst-Timor", "østtimores"
  ]
LDC_termlist_trunc = ["Mali", "malian", "malier", "maliar", "malisk"]
LDC_termlist_caps = ["LEDC", " MUL "]

LDC_phrase = r'(?:{})'.format('|'.join(LDC_termlist))
LDC_phrase_trunc = r'\b(?:{})\b'.format('|'.join(LDC_termlist_trunc))
LDC_phrase_caps = r'(?:{})'.format('|'.join(LDC_termlist_caps))

SIDS_termlist = [
  "small-island developing nation", "small-island developing stat", "small-island developing countr",
  "small island developing nation", "small island developing stat", "small island developing countr",
  "Antigua and Barbuda", "Antigua & Barbuda", "antiguan", "Bahamas", "bahamian", "Bahrain", "Barbados", "barbadian", "Belize", "Cabo Verde", "Cape Verde", "Comoros", "comoro islands", 
  "iles comores", "Cuba", "Dominica", "Micronesia", "Fiji", "Grenada", "Guinea-Bissau", "bissau-guinean", "Guyana", "guyan", "Haiti", "Jamaica", "Kiribati", "Maldives", "maldivian", "Marshall Islands", "Mauritius", "mauritian", "Nauru", "Palau", "Papua New Guinea", "Saint Kitts and Nevis", "st kitts and nevis", 
  "Saint Lucia", "St Lucia", "St. Vincent and the Grenadines", "Saint Vincent and the Grenadines", "Vincent & the Grenadines", "Samoa", "Sao Tome", "Seychelles", "seychellois", "Singapore", "Solomon Islands",
  "Surinam", "Timor-Leste", "timorese", "Tonga", "Trinidad and Tobago", "Trinidad & Tobago", "trinidadian", "tobagonian", "Tuvalu", "Vanuatu", 
  "Anguilla", "Aruba", "Bermuda", "Cayman Islands", "Northern Mariana", "Cook Islands", "Curacao", "French Polynesia", "Guadeloupe", "Guam", "Martinique", 
  "Montserrat", "New Caledonia", "Niue", "Puerto Rico", "puerto rican", "Sint Maarten", "Turks and Caicos", "Turks & Caicos", "Virgin Islands", 

  "små utviklingsøystat","små øystat",
  "Antigua og Barbuda", "bahaman", "barbader", "barbadar", "barbadisk", "belizisk", "Kapp Verde", "kappverd", "Komor", "Den Dominikanske Republikk", "Mikronesi", "grenadi", "bissauguinean", "jamaikan", "Maldivene", "maldiver", "maldivisk", "maldivar", "Marshalløyene", "Papua Ny-Guinea", "papuan", "Saint Kitts og Nevis", 
  "sankkitt", "Saint Vincent og Grenadine", "sanktvinsent", "seychell", "saotomes", "singapor", "Salomonøy", "salomoner", "salomonsk", "salomonar", "Øst-timor", "østtimores", "Trinidad og Tobago", "trinidader", "trinidadar", "trinidadisk", "tuvaler", "tuvalar", "tuvalsk", "vanuatisk", "bermudisk", "Caymanøyene", "caymansk", "Nord-Marianene", "Cookøyene", "Fransk Polynesia", "polynesisk", "Ny-Caledonia", "kaledon", "martinikan", "Turks- og Caicosøyene", "ny-caledonia", "nykaledon", "puertorikan", "Jomfruøyene"
  ]
SIDS_termlist_caps = ["SIDS"] #can us with "case=TRUE" but watch out for medical SIDS (sudden infant death syndrome)

SIDS_phrase = r'(?:{})'.format('|'.join(SIDS_termlist))
SIDS_phrase_caps = r'(?:{})'.format('|'.join(SIDS_termlist_caps))

LDS_termlist = [
  "landlocked developing nation", "landlocked developing stat", "land-locked developing nation", "land-locked developing stat", 
  "Afghanistan", "afghan", "Armenia", "Azerbaijan", "Bhutan", "bhutanese", "Bolivia", "Botswana", "Burkina Faso", "Burundi", "Central African Republic", "Chad",
  "Eswatini", "eswantian", "Ethiopia", "Kazakhstan", "kazakh", "Kyrgyzstan", "Kyrgyz", "kirghizia", "kirgizstan", "Lao People’s Democratic Republic",
  "Laos", "Lesotho", "Malawi", "malawian", "Mali", "Mongol", "Nepal", "Niger", "North Macedonia", "Republic of Macedonia", "Paraguay", "Moldova", "Rwanda", 
  "South Sudan", "sudanese", "Swaziland", "Tajikistan", "tadjikistan", "tajikistani", "Turkmenistan", "Uganda", "Uzbekistan", "uzbekistani", 
  "Zambia", "zambian", "Zimbabwe", 

  "kystløse utviklingsland",
  "armensk", "armener", "armenar", "Aserbajdsjan", "Den Sentralafrikanske republikk", "sentralafrikan", "Tsjad", "Etiopia", "etiopier", "etiopiar", "etiopisk", 
  "Kasakhstan", "Kirgisistan", "kirgiser", "kirgisar", "kirgisisk", "laot", "laotisk", "lesothisk", "Nord-Makedonia", "makedon", 
  "moldover", "rwander", "rwandisk", "Tadsjikistan", "Sør-sudan", "Tadsjikistan", "tadsjiker", "tadsjikar", "tadsjikisk", "turkmener", "turkmenar", "turkmensk",
  "Usbekistan", "usbeker", "usbekar", "usbekisk", "zambier", "zambiar", "zambisk", "zimbabwisk"]
LDS_termlist_trunc = ["Mali", "malian", "malier", "maliar", "malisk"]

LDS_phrase = r'(?:{})'.format('|'.join(LDS_termlist))
LDS_phrase_caps = r'(?:{})'.format('|'.join(LDS_termlist_trunc))

LMIC_termlist = [
  "least developed countr", "least developed nation", "developing countr", "developing nation", "developing states", "island developing state", "developing world", 
  "less developed countr", "less developed nation", 
  "under developed countr", "under developed nation", "underdeveloped countr", "underdeveloped nation",
  "underserved countr", "underserved nation", "deprived countr", "deprived nation",
  "middle income countr", "middle income nation", "middle-income countr", "middle-income nation", 
  "low income countr", "low income nation", "lower income countr", "lower income nation", "low-income countr", "low-income nation", "lower-income countr", "lower-income nation", 
  "poor countr", "poor nation", "poorer countr", "poorer nation", 
  "third world", "global south", "transitional countr", "emerging economies", "emerging nation", 
  
  "utviklingsland", "u-land", "uland", "underutviklede land", "underutvikla land", "lavinntektsland", "låginntektsland",
  "underpriviligerte land", "mellominntektsland", "ressurssvake land", "tredje verd", "fattige land", 
  "globale sør", "overgangsøkonomi", "fremvoksende økonomier", "framvoksende økonomier", "framveksande økonomi"
  "framvoksende land", "fremvoksende land", "framveksande land", "bistandsland", "minst utviklede land", "små utviklingsøystat", "små øystat",
  "kystløse utviklingsland",
  
  "Angola", "Benin", "Burkina Faso", "Burkina fasso", "burkinese", "burkinabe", "Burundi", "Central African Republic", "central african", 
  "Comoros", "comoro islands", "iles comores", "Congo", "Djibouti", "Eritre", "Ethiopia", "Gambia", "Guinea",
  "Lesoth", "Liberia", "Madagas", "Malawi", "Mauritan", "Mozambi", "Niger", "Rwanda", "Sao Tome", 
  "Senegal", "Sierra Leone", "Somalia", "Sudan", "Togo", "tongan", "Uganda", "Tanzania", "Zambia", "Cambodia", "Kiribati", 
  "Lao People", "Laos", "myanma", "Solomon islands", "Timor Leste", "timorese", "Tuvalu", "Vanuatu", 
  "afghan", "Bangladesh", "Bhutan", "Nepal", "Yemen", "Haiti", 
  
  "gambisk", "gambier", "gambiar", "Den Sentralafrikanske republikk", "sentralafrikan", "Tsjad", "Komor", "Kongo", "Etiopi", "bissauguinean", 
  "lesothi", "liberisk", "gassisk", "Mosambik", "Sao Tome og Principe", "saotomes", "Kambodsja", "Salomon", "Øst-Timor", "østtimores"
  
  "Antigua", "Barbuda", "Bahamas", "bahamian", "Bahrain", "Barbados", "barbadian", "Belize", "Cabo Verde", "Cape Verde", 
  "Cuba", "Dominica", "Micronesia", "Fiji", "Grenada", "Guyana", "Haiti", "Jamaica", "Maldiv", "Marshall Islands", "Mauriti", "Nauru", "Palau", 
  "Saint Kitts", "st kitts", "Saint Lucia", "St Lucia", "Vincent and the Grenadines", "the Grenadines", "Samoa", "Sao Tome", "Seychell", "Singapore", 
  "Surinam", "Tonga", "Trinidad", "Tobago", "Anguilla", "Aruba", "Bermuda", "Cayman Islands", "Northern Mariana", "Cook Islands", "Curacao", "French Polynesia", 
  "Guadeloupe", "Guam", "Martinique", "Montserrat", "New Caledonia", "Niue", "Puerto Ric", "Sint Maarten", "Turks and Caicos", "Turks & Caicos", "Virgin Islands", 
  
  "Kapp Verde", "Den Dominikanske Republikk", "Mikronesi", "Marshalløy", "Vincent og Grenadine", "Nord-Marian", "Cookøy", 
  "Fransk Polynesia", "Ny-Caledonia", "Turks- og Caicosøy", "Jomfruøy",
  
  "Afghan", "Armenia", "Azerbaijan", "Bhutan", "Bolivia", "Botswana", "Burkina Faso", "Burundi", "Chad", 
  "Eswatini", "eswantian", "Kazakhstan", "Kyrgyzstan", "kirghiz", "Mongol", "Nepal", "North Macedonia", "Republic of Macedonia", "Paraguay", "Moldov", "Rwand", 
  "Swazi", "Tajikistan", "tadjikistan", "Turkmenistan", "Uganda", "Uzbekistan", "Zambia", "Zimbabwe", 
  
  "armensk", "armener", "armenar", "Aserbajdsjan", "Kasakhstan", "Kirgis", "Nord-Makedon", "Tadsjik", "Usbek", "zambisk", "zambier", "zambiar",
  
  "Albania", "Algeria", "Argentin", "Bahrain", "Belarus", "Byelarus", "Belorussia", "Hondura", "dahomey", "Bosnia", "Herzegovina", 
  "Botswan", "Bechuanaland", "Brazil", "Brasil", "Bulgaria", "Upper Volta", "Kampuchea", "Khmer Republic", "Cameroon", "Cameroun", "Ubangi Shari", "Chile", 
  "China", "Chinese", "Colombia", "Costa Rica", "Cote d’Ivoire", "Cote d Ivoire", "Ivory Coast", "Croatia", "Cyprus", "cypriot", "Czech", 
  "Ecuador", "Egypt", "United Arab Republic", "El Salvador", "Estonia", "Gabon", "Ghana", "Gibralta", "Greece", "greek", "Hondura", "Hungary", "hungarian", 
  "India", "Indonesia", "Iran", "Iraq", "Isle of Man", "Jordan", "Kenya", "Korea", "Kosovo", "kosovan", "Latvia", "Lebanon", "lebanese", "Libya", "Lithuania", 
  "Macau", "Macao", "macanese", "malagasy", "Malaysia", "Malay Federation", "Malaya Federation", "Malta", "maltese", "Mexico", "mexican", "Montenegr",
  "Morocco", "moroccan", "Namibia", "Netherlands Antilles", "Nicaragua",  "Oman", "Muscat", "Pakistan", "Panama", "Peru", "Philippine", "Philipine", "Phillipine", 
  "Phillippine", "filipino", "filipina", "Poland", "polish", "Portugal", "portugese", "Romania", 
  "Russia", "Polynesia", "Saudi Arabia", "Serbia", "Slovakia", "Slovak Republic", "Slovenia", "Melanesia", "South Africa", "Sri Lanka", "Dutch Guiana", 
  "netherlands guiana",  "syria", "thai", "tunisia", "ukrain", "uruguay", "venezuela", "vietnam", "west bank", "gaza", "palestin", 
  "Yugoslavia", "Turkey", "turkish", "Georgia",
  
  "Algerie", "Hviterussland", "Kviterussland", "Bosnia-Hercegovina", "Øvre Volta", "Kamerun", "Elfenbenskysten", "Elfenbeinskysten", "Kroat", "Kypros", 
  "kypriot", "Tsjekki", "Arabiske Emirat", "Estland", "estisk", "Hellas", "gresk", "greker", "grekar", "Ungarn", "ungarsk","ungarer", "ungarar", "Irak", "Libanon", 
  "libanes", "Litau", "Marokko", "marokkan", "Nederlandske Antill", "Filippin", "Polen", "polsk", "polakk", "Russland", "russisk", "russer", "russar", "Sør-Afrika", 
  "Vestbredden", "Vestbreidda", "Tyrkia", "tyrkisk", "tyrker", "tyrkar"
  ]
LMIC_termlist_trunc = ["kina", "Mali", "malian", "malier", "maliar", "malisk"]
LMIC_termlist_caps = ["LEDC", " MUL ", "SIDS", "LMIC", "LAMI "] #can use with "case=TRUE" but watch out for double meanings (medical SIDS)
#space after "LAMI" is on purpose (always followed by country, nation etc.)
#"polish" might cause problems
#"gasser" (Norwegian for people from Madagascar) is omitted due to noise (in Norwegian)

LMIC_phrase = r'(?:{})'.format('|'.join(LMIC_termlist))
LMIC_phrase_trunc = r'\b(?:{})\b'.format('|'.join(LMIC_termlist_trunc))
LMIC_phrase_caps = r'(?:{})'.format('|'.join(LMIC_termlist_caps))
```


```python
Data["LDCs"] = (
    (Data['result_title'].str.contains(LDC_phrase, na=False, case=False))
    |(Data['result_title'].str.contains(LDC_phrase_trunc, na=False, case=False))
    |(Data['result_title'].str.contains(LDC_phrase_caps, na=False, case=True))
)
print("Number of results mentioning LDCs = ", len(Data.loc[Data['LDCs']])) 


Data["SIDS"] = (
    (Data['result_title'].str.contains(SIDS_phrase, na=False, case=False))
    |(Data['result_title'].str.contains(SIDS_phrase_caps, na=False, case=True))
)
print("Number of results mentioning SIDS = ", len(Data.loc[Data['SIDS']])) 


Data["LDS"] = (
    (Data['result_title'].str.contains(LDS_phrase, na=False, case=False))
    |(Data['result_title'].str.contains(LDS_phrase_caps, na=False, case=True))
)
print("Number of results mentioning LDS = ", len(Data.loc[Data['LDS']])) 


Data["LMICs"] = (
    (Data['result_title'].str.contains(LMIC_phrase, na=False, case=False))
    |(Data['result_title'].str.contains(LMIC_phrase_trunc, na=False, case=False))
    |(Data['result_title'].str.contains(LMIC_phrase_caps, na=False, case=True))
)
print("Number of results mentioning LMICs = ", len(Data.loc[Data['LMICs']]))
```


```python
Data["LDCSIDS"] = (Data["SIDS"]|Data["LDCs"])

print("Number of results mentioning LDCs or SIDS = ", len(Data.loc[Data['LDCSIDS']]))
```

## SDG 1

### SDG 1.1

*1.1 By 2030, eradicate extreme poverty for all people everywhere, currently measured as people living on less than $1.25 a day*

*Innen 2030 utrydde all ekstrem fattigdom*


```python
#Term lists
termlist1_1 = ["extreme poverty", "severe poverty", "deep poverty", "abject poverty", "absolute poverty", "destitution", "global poverty", "international poverty",
              "ekstrem fattigdom", "global fattigdom", "internasjonal fattigdom"
              ]

phrasedefault1_1 = r'(?:{})'.format('|'.join(termlist1_1))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault1_1, na=False, case=False))
    ),"tempsdg01_01"] = "SDG01_01"

print("Number of results = ", len(Data[(Data.tempsdg01_01 == "SDG01_01")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_01 == "SDG01_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 1.2

*1.2 By 2030, reduce at least by half the proportion of men, women and children of all ages living in poverty in all its dimensions according to national definitions*

*Innen 2030 minst halvere andelen menn, kvinner og barn i alle aldre som lever i fattigdom, i henhold til nasjonale definisjoner*



```python
#Termlists
termlist1_2a = ["anti-poverty", "antipoverty", "out of poverty", "poverty", "rural poor", "urban poor", "working poor",
              "fattigdom"
              ]

termlist1_2b = ["låginntekt", 'låg inntekt',"fattig"]
#Only Norwegian used here - in English, "low income" is combined like "poor" (2d) - if not, there are too many irreleavnt results about "low income countries" 

termlist1_2c = ["household", "people", "communit", "child", "relief", "family", "families",
              "hushold", "hushald", "folk", "samfunn", "barn", "born", "famili"
              ]

termlist_2d = ["poor household", "poor people", "poor communit", "poor child", "poor famil", "poor relief",
               "low income household", "low-income household","low income people", "low-income people","low income communit", "low-income communit","low income famil", "low-income famil"
              ]
#Testing revealed that "poor" AND people terms mostly found medical results (e.g. "children of mothers with poor iodine intake"), therefore "poor" is combined in phrases. This is only an issue in English.
#In the same way, "low income" is combined like "poor" - without doing so, there are too many results about "low income countries" 

phrasedefault1_2a = r'(?:{})'.format('|'.join(termlist1_2a))
phrasedefault1_2b = r'(?:{})'.format('|'.join(termlist1_2b))
phrasedefault1_2c = r'(?:{})'.format('|'.join(termlist1_2c))
phrasedefault1_2d = r'(?:{})'.format('|'.join(termlist_2d))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault1_2a, na=False, case=False))
    | ((Data['result_title'].str.contains(phrasedefault1_2b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault1_2c, na=False, case=False)))
    | (Data['result_title'].str.contains(phrasedefault1_2d, na=False, case=False))
    ),"tempsdg01_02"] = "SDG01_02"

print("Number of results = ", len(Data[(Data.tempsdg01_02 == "SDG01_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_02 == "SDG01_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 1.3

*1.3 Implement nationally appropriate social protection systems and measures for all, including floors, and by 2030 achieve substantial coverage of the poor and the vulnerable*

*Innføre nasjonalt tilpassede sosiale velferdsordninger og tiltak for alle, inkludert minstestandarder, og innen 2030 oppnå en vesentlig dekning av fattige og sårbare*

Here the phrases used in WOS syntax have been merged. In the title and abstract search, the target was split into phrases because some of the terms worked well alone, but others were too general and thus were used combined with "poor and vulnerable" groups (see documentation in the WOS strings for how these were established). This was done even though the target applies to all people. However, here, with the title search, we do not think that this restriction is needed, and therefore is removed. 

We have also included some Norwegian-specific terminology/names for social support schemes, such as "frikort", "folketrygd" and "NAV" (Norwegian Labour and Welfare Administration; https://www.nav.no/en/home/about-nav/what-is-nav).



```python
#Termlists
termlist1_3a = ["welfare system", "welfare service", "social security", "social service", "social assistance", "social floor", 
                "social safety net", "safety net program",
                "social protection", "social benefits" , "social insurance", "social care service",
                "basic income" , "income security" , "guaranteed income" , "living allowance" , "housing assistance",
                "cash benefit" , "cash transfer", "cash plus program",
                "school feeding" , "free school meal" , "food stamp program" , "nutrition assistance program" , "food assistance program" , "WIC program" , "WIC benefits",
                "labour market polic" , "labor market polic" , "labour market intervention" , "labor market intervention", "labour market program" , "labor market program" , "public works program",
                "unemployment benefit" , "unemployment compensation" , "unemployment insurance" , "unemployment allowance" , 
                "disability benefit" , "disability allowance" , "disability pension" , "disability tax credit" , "disability insurance", 
                "health care benefit" , "sickness benefit" , "sick benefit" , "sick pay" , "paid sick leave" , "paid medical leave" , "sickness allowance",
                "maternity pay" , "maternity insurance" , "maternity benefit" , "maternity allowance" , "paid maternity leave" , 
                "parental benefit" , "paid parental leave" , "paid family leave" , "family leave tax credit" , "parental leave tax credit",
                "child benefit" , "child tax credit" , "child allowance",
                "pension insurance" , "pension plan" , "pension benefit" , "public pension" , "state pension",
                
                "velferdssystem", "velferdstjeneste", "velferdsteneste", "velferdsgode", "velferdsordning", "velferdsmodell", "velferdspolitikk", 
                "folketrygd", "trygdeordning", "sikkerhetsnett", "trygderett", 
                "sosialpolitiske ordning", "sosialhjelp",
                "gratis skolemat", "gratis skolemåltid",
                "arbeidsledighetstrygd", "arbeidsløysetrygd", "alderspensjon", "uførepensjon", "sykepenger", "sjukepengar", "frikort",
                "barnetrygd", "foreldrepermisjon", "svangerskapspermisjon", "foreldrefradrag", "foreldrefrådrag", "foreldrepenger", "fedrekvote", "mødrekvote"
              ]
#"sikkerhetsnett"(NO) is quite a general term but works ok

termlist1_3b = ["NAV "] #for searching with case=TRUE. "NAV"(NO) is the local Norwegian welfare agency


phrasedefault1_3a = r'(?:{})'.format('|'.join(termlist1_3a))
phrasedefault1_3b = r'(?:{})'.format('|'.join(termlist1_3b))

```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault1_3a, na=False, case=False))
    | (Data['result_title'].str.contains(phrasedefault1_3b, na=False, case=True))
    ),"tempsdg01_03"] = "SDG01_03"

print("Number of results = ", len(Data[(Data.tempsdg01_03 == "SDG01_03")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_03 == "SDG01_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 1.4

*1.4 By 2030, ensure that all men and women, in particular the poor and the vulnerable, have equal rights to economic resources, as well as access to basic services, ownership and control over land and other forms of property, inheritance, natural resources, appropriate new technology and financial services, including microfinance*

*Innen 2030 sikre at alle menn og kvinner, særlig fattige og sårbare, har lik rett til økonomiske ressurser og tilgang til grunnleggende tjenester, til å eie og kontrollere jord og andre former for eiendom, og til arv, naturressurser, ny teknologi og finansielle tjenester, inkludert mikrofinansiering*

Like 1.3, many of the terms in the target were quite general. So although the target interpretation was for all people, to make the string find relevant results in an abstract search we combined all 3 phrases with "poor and vulnerable" groups (see documentation in the WOS strings for how these were established). However, here, with the title search, we do not think that this restriction is needed, and therefore is removed. 

#### Phrase 1


```python
#Termlists

termlist1_4a = ["financial inclusion", "unbanked",
                "microfinanc", "micro-financ", "microinsurance", "micro-insurance", "microcredit", "micro-credit", "microloan", "micro-loan",
                "mikrofinans", "mikrokreditt", "mikroinnskudd", "mikroforsikring"
              ]

termlist1_4b = ["access" , "equitab" , "equity" , "equality" , "equal", 
                "ownership" , "control" , "right" , "empower" , "inclusion",
                "affordab" , "pro poor" , "pro-poor", "inexpensive" , "free of charge" , "free service",
                "inaccessib" , "barrier" , "obstacle" , "unequal" , "inequalit" , "inequitab" , "exclusion", 
                "unaffordab" , "expensive",

                "tilgang", "tilgjenge", "likestilling", "likhet", "likheit", "rettferd", "rettvis",
                "kontroll", "rettighet", "rettigheit", "inkludering", "inkluderende", "inkluderande", "ekskludering", "marginalis", "myndiggjør", "myndiggjer",
                "dyre", "ikke råd", "ikkje råd"
                ] 
                #"equity" etc. will cover "inequity" due to automatic truncation

termlist1_4c = ["a bank" , "bank account" , "banking" , "bank services", "financial service", "monetary service", "economic service",
                "digital finance", "mobile money", "electronic payment", "digital payment", "fintech",
                "credit", "savings account", "insurance", "payment service", "transfer service", "transfer fund",
                "financial resource", "monetary resource", "economic resource", "financial asset", "economic asset", "financial opportunit",

                "bankkonto", "bankkunde", "sparebank", "banktjenester", "finansielle tjenester", "banktenester", "finansielle tenester",
                "kreditt", "lån", "sparekonto", "forsikring", "betalingsløsning", "betalingsløysing", "betalingstjeneste", "betalingsteneste", "digitale penger", "digitale pengar", "nettbank", "mobilbank",
                "finansielle ressurs", "økonomiske ressurs"
                ]
#"Saving" (="sparing" NO) are not used here as they mostly add noise from "energy saving", "cost savings" or "nerve-sparing" (medical). "seed banks" are also an issue. 

phrasedefault1_4a = r'(?:{})'.format('|'.join(termlist1_4a))
phrasedefault1_4b = r'(?:{})'.format('|'.join(termlist1_4b))
phrasedefault1_4c = r'(?:{})'.format('|'.join(termlist1_4c))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault1_4a, na=False, case=False))
    | ((Data['result_title'].str.contains(phrasedefault1_4b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault1_4c, na=False, case=False)))
    ),"tempsdg01_04"] = "SDG01_04"

print("Number of results = ", len(Data[(Data.tempsdg01_04 == "SDG01_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_04 == "SDG01_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Term lists

termlist1_4d = ["access" , "equitab" , "equity" , "equality" , "equal", 
                "ownership" , "control" , "right" , "empower" , "inclusion", "sharing",
                "affordab" , "pro poor" , "pro-poor", 
                "inaccessib" , "barrier" , "obstacle" , "unequal" , "inequalit" , "inequitab" , "exclusion",
                "unaffordab" , "expensive", "insecurity",
                "land rental", "income security", "secure livelihood",

                "tilgang", "tilgjenge", "likestilling", "ulikhet", "rettferd", "rettvis", 
                "eierskap", "eigarskap", "kontroll", "rettighet", "rettigheit", "ekskludering", "marginali", "myndiggjør", "myndiggjer",
                "dyre", "ikke råd", "ikkje råd", "sikkerhet", "sikkerheit", "usikker",
                "eiendomsrett", "eigedomsrett", "landrett", "landfattig", "jobbtrygghe", "arvesystem"
                ]
                #We removed "inkludering"(NO) because the results were about using farms in inclusive education

termlist1_4e = ["economic resource.*", "natural resources",
                "employment", "decent work", "paid work", "labour market", "incomes", "livelihood", "livelihoods", "wealth", "inheritance", "utkomme", "utkome", 
                "farmland.*", "land resources", "farm", "farms", "tenure", "property", "home ownership",

                "finansielle ressurs.*", "økonomiske ressurs.*", "naturressurs.*",
                "lønnet arbeid", "løna arbeid", "anstendig arbeid.*", "arbeidsmark.*", "inntekt", "lønn", "levebrød", "underhold", "underhald", "rikdom", "arv", "arving",
                "gård", "småbruk", "familiegård", "gårdsbruk", "gardsbruk", "dyrket mark", "dyrka mark", "dyrkamark", "kultivert mark", "landsressurs.*", 
                "eiendom.*", "eigedom.*", "forpakting"
                ]
                #Here we are preventing truncation because "arv"(NO) is problematic. 
                #We don't use "land" by itself, because in Norwegian it throws up mostly noise (it means country). Specific terms with "land" are added in 4f.
                #We also had to remove the term "income" and specify it as "income inequality" under 4f. This was because there were many results about e.g. health outcomes of a disease in a low-income country.

termlist1_4f = ["land rights", "rights to land", "right to land", "access to land", "land grab", "tenure security", "secure tenure", "income inequality", 
                "rettigheter til land", "rettigheiter til land", "rett til land", "jordleie", "jordleige", "leie av jord", "tomtefeste",
                "bygsling", "tomterett", "servitutt"
                ]

termlist1_4g = ["intellectual property right", "wind farm", "quality control", "parasite control", "worm control", "pest control"] 
#These are terms that we want to remove, that create noise (NOT search)

phrasedefault1_4d = r'(?:{})'.format('|'.join(termlist1_4d))
phrasespecific1_4e = r'\b(?:{})\b'.format('|'.join(termlist1_4e))
phrasedefault1_4f = r'(?:{})'.format('|'.join(termlist1_4f))
phrasedefault1_4g = r'(?:{})'.format('|'.join(termlist1_4g))
```


```python
#Search 
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault1_4f, na=False, case=False))
        |((Data['result_title'].str.contains(phrasespecific1_4e, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault1_4d, na=False, case=False)))
    ) 
    & (~Data['result_title'].str.contains(phrasedefault1_4g, na=False, case=False))
),"tempsdg01_04"] = "SDG01_04"

print("Number of results = ", len(Data[(Data.tempsdg01_04 == "SDG01_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_04 == "SDG01_04"), ("result_id", "subcategory", "result_title", "SDG_action", "SDG_topic_wos", "mentionssdgno", "tempsdg01_04")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Term lists

termlist1_4h = ["access" , "equitab" , "equity" , "equality" , "equal", "empower" , "inclusion", 
                "ownership", "right",
                "affordab" , "pro poor" , "pro-poor", "inexpensive", "unaffordab" , "expensive", "low cost", "free of charge", "free service",
                "inaccessib" , "barrier", "inequalit", "inequitab", "exclusion",

                "tilgang", "tilgjenge", "likestilling", "ulikhet", "rettferd", "rettvis", "myndiggjør", "myndiggjer",
                "eierskap", "eigarskap", "rettighet", "rettigheit",
                "ikke råd", "ikkje råd",
                "ekskludering"
                ]
                #We removed "inkludering"(NO) because the results were about using farms in inclusive education             

termlist1_4i = ["basic service", "basic facilities", "essential service",
                "drinking water", "sanitation", "basic hygiene", "hygiene service", "toilet", "handwashing", "sewage", "WASH facilities", 
                "clean water",
                "waste collection", "waste service", "waste facilit", "garbage service", "garbage collection", 
                "health service", "health facilit", "basic health", "essential health", "healthcare", "health care", "medical care", "essential medical",
                "school service", "school facilit", "basic school", "primary school", "basic education", "education service", "primary education",
                "basic communication service", "basic telecommunication service", "basic information service", "basic information infrastructure",
                "electricity", "energy service", "modern energy", "clean fuel", "clean energy", "modern energy",
                "public open space", "public space", "public green space",
                "basic mobility", "urban mobility", "rural mobility", "all-season road", "transport service", "public transport",

                "grunnleggende tjeneste", "grunnleggjande teneste", "greunnleggende fasilitet", 
                "drikkevann", "drikkevatn", "grunnleggende hygiene", "grunnleggjande hygiene", "kloakk", "toalett", "vannklosett", "vassklosett", "håndvask", "handvask", "sanitær",
                "rent vann", "reint vatn", "reint vann", "innlagt vann", "innlagt vatn", "vanntilgang", "vannforsyning",
                "avfallstjeneste", "avfallsteneste", "søppeltømming", "avfallsinnsamling", "bosteneste", "bosinnsamling", "bostømming", "renovasjon",
                "helsetjeneste", "helseteneste", "fastlege","helsevesen",
                "ungdomsskole", "ungdomsskule", "barneskole", "barneskule", "grunnleggende utdannin", "grunnleggjande utdannin", 
                "kommunikasjonstjenester", "kommunikasjonstenester", "kommunikasjonsinfrastruktur", "grunnleggende kommunikasjon",
                "energitjeneste", "energiteneste", "energilever", "elektrisitet", "energiforsyning", "kraftforsyning", "moderne energi",
                "offentlig rom", "offentlige rom", "offentlege rom", "offentlege rom", "grønt areal", "grønne areal", "grøntområde", "friområde", "friareal", "rekreasjonsområde",
                "offentlig transport", "offentlige transport", "offentleg transport", "offentlege transport", "kollektivtransport", "kollevktivtilb", "transport ordning", 
                "mobilitet"
                ] #"skole"(NO) is limited to specific basic levels here to avoid its use in Norwegian university names, e.g. "Høyskole"

termlist1_4jnot = ["Authenticated Access", "Access Control"]
#terms from ICT that are used a lot in healthcare (i.e. technical access and security) that we want to remove

phrasedefault1_4h = r'(?:{})'.format('|'.join(termlist1_4h))
phrasedefault1_4i = r'(?:{})'.format('|'.join(termlist1_4i))
phrasedefault1_4jnot = r'(?:{})'.format('|'.join(termlist1_4jnot))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault1_4h, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault1_4i, na=False, case=False))
),"tempsdg01_04"] = "SDG01_04"

print("Number of results = ", len(Data[(Data.tempsdg01_04 == "SDG01_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_04 == "SDG01_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 1.5

*1.5 By 2030, build the resilience of the poor and those in vulnerable situations and reduce their exposure and vulnerability to climate-related extreme events and other economic, social and environmental shocks and disasters*

*Innen 2030 bygge opp motstandskraften til fattige og personer i utsatte situasjoner, slik at de blir mindre utsatt for og mindre sårbare for klimarelaterte ekstremhendelser og andre økonomiske, sosiale og miljømessige påkjenninger og katastrofer*

Here under terms for indigenous and minority groups, we have included Norwegian-specific groups (source: Utdanningsdirektoratet (n.d.) Nasjonale minoriteter. https://www.udir.no/laring-og-trivsel/nasjonale-minoriteter/hva-er-en-nasjonal-minoritet/ (accessed Nov 2022))



```python
#Termlists

termlist1_5a = ["sendai", "protect", "safeguard", "safety", "safety net", "social protection", "social floor", "social security",
                "coping", "cope", "adapt", "resilien", "mitigat", "prepared", "protection", "early warning", "impact", "vulnerab", "exposure",
                # "disaster strateg", "disaster relief", "disaster manag", "disaster polic", "medical respon", "risk plan", "risk strateg", "risk manag", "risk polic",
                "planning", "disaster plan", "strateg", "disaster reduc", "risk reduc", "relief", "manag", "program", "programme", "policy", "policies", 
                "medical response", "medical respond", "emergency respon",

                "beskytte", "verne", "sikkerhet", "sikkerheit", "sosialpolitiske ordning", "sosialhjelp",
                "tåle", "tilpass", "forbered", "beredskap", "varsling", "varsel", "sårbar", "eksponer", "påvirkning", "påverknad",
                "handlingsplan", "planer", "planar", "planlegging", "katastrofeplanlegging", "krisehandtering", "krisehåndtering", "risikoreduksjon", "strategi", "politikk", "retningslinj",
                "nødhjelp", "naudhjelp", "feltsykehus", "feltsjukehus"
                ]
                #terms commented out are already covered by other terms

termlist1_5b = ["disaster", "catastrophe", "hazard",
                "extreme climat", "extreme weather", "extreme precipitation", "extreme rain", "extreme snow", "extreme temperatur", "extreme storm", "extreme wind", 
                 "rogue wave", "tsunami", "cyclone", "typhoon", "hurricane", "tornado", 
                 "drought", "flood", 
                 "avalanche", "landslide", "land-slide", "land slide", "rockslide", "rock-slide", "rock slide", "rockfall", "surface collapse", "mudflow", "mud-flow", 
                 "cold spell", "cold wave", "dzud", "blizzard", "snowstorm", 
                 "heatwave", "heat-wave", 
                 "earthquake", "volcan", "ash cloud", "ash fall", "tephra", 
                 "wildfire", "wild-fire", "wild fire", "forest-fire", "forest fire", "forestfire", 
                 "sea-level rise", "sea-level change", "rising sea-level", 
                 "outbreak", "pandemic", "epidemic", 
                 "armed conflict", "political instability", "civil instability", "politically volatile", 
                 "unrest", "financial crash", "financial shock", "economic downturn", "economic shock",
                
                "katastrof", "krise", 
                 "ekstremvær", "ekstremver", 
                 "tropisk lavtrykk", "tropisk lågtrykk", "flodbølg", "monsterbølg", "ekstrembølg", 
                 "orkan",  "tyfon", "syklon", "snøstorm", 
                 "flom", "flaum", "oversvøm", "ovefløym", "tørke", 
                 "snøskred", "skred", "snøras", "lavine", "jordskred", "jordras", "sørpeskred", "leirras", "leirskred", "steinras", "steinskred", "synkehull", 
                 "uvanlig kulde", "uvanlig kaldt", "uvanleg kulde", "uvanleg kaldt", "ekstrem kuld", "ekstremkuld", "kuldebølg", "snøstorm", 
                 "varmebølg", "hetebølg", "ekstrem varm", "ekstremvarm", "uvanlig varm", "uvanleg varm", 
                 "jordskjelv", "vulkan", "askenedfall", "oskenedfall", "askesky", "oskesky", 
                 "skogbrann", "gressbrann", "grasbrann", "lyngbrann", 
                 "havnivåstigning", "stormflo", 
                 "pandemi", "epidemi", "utbrudd", "utbrot",
                 "politisk ustabilitet", "væpnede konflikter", "væpnet konflikt", "væpna konflikt", "borgerkrig", "borgarkrig", "fremmedkrig", "finanskrise", "finanssjokk", 
                 "finanskatastrofe", "finanskræsj", "økonomisk nedgang", "økonomisk sjokk", "økonomisk katastrofe"
                ] 

termlist1_5c = ["war", "wars", 
                "krig", "ras"]  #terms from 5b where we need to prevent truncation (lots of "etterkrigstid"(NO))

termlist1_5d = ["poverty", "rural poor", "urban poor", "working poor", "destitute", "low income", "low-income", "poor households", "poorest households", "poor communit", "poorest communit", 
                "social capital",
                "disadvantaged", "marginalis", "marginalized", "vulnerable", "discriminated",
                "slum", "shanty town", "informal settlement", "homeless",
                "patient", "disabled", "disabilities", "disability",
                "older people", "old people", "retired people", "elderly", "elders", "pensioner", 
                "unemployed",
                "women", "woman", "girl", "pregnan", "maternity", "child", "baby", "babies", "newborn", "toddler", "youth", "infant",
                "indigenous", "minorities", "minority", "refugee", "asylum", "immigrant",
                "trans people", "transgender", "lgbt", "lesbian", "gay", "bisexual", "intersex",
                "least developed countr", "least developed nation", "developing countr", "developing nation", "developing states", "island developing state", "developing world", 
                "less developed countr", "less developed nation", 
                "under developed countr", "under developed nation", "underdeveloped countr", "underdeveloped nation",
                "underserved countr", "underserved nation", "deprived countr", "deprived nation",
                "middle income countr", "middle income nation", "middle-income countr", "middle-income nation", 
                "low income countr", "low income nation", "lower income countr", "lower income nation", "low-income countr", "low-income nation", "lower-income countr", "lower-income nation", 
                "poor countr", "poor nation", "poorer countr", "poorer nation", 
                "third world", "global south", "transitional countr", "emerging economies", "emerging nation", 

 
                "fattig", "lavinntekt", "lav inntekt", "låginntekt", "låg inntekt",
                "sårbar", "diskrimin",
                "hjemløs","heimlaus",
                "pasient", "uføre", "funksjonshem",
                "eldre", "de gamle", "dei gamle",
                "arbeidsløs","arbeidslaus",
                "kvinne", "jente", "gravid", "barn", "born", "babier", "nyfødt","nyfødd",
                "urfolk", "urinnvånarar", "urbefolkning", "urinnvånere", "sápmi", "sami", "minoritet", "jøder", "jådar", "kvener", "kvenar", "norskfinn", "skogfinn", "romani", "tatere", "taterar", "asylsøk", "flyktning", "innvandrer", "innvandrar",
                "transperson", "lesbisk", "homofile", "bifile", "lbht", "interkjønn",
                "utviklingsland", "u-land", "uland", "underutviklede land", "underutvikla land", "lavinntektsland", "låginntektsland",
                "underpriviligerte land", "mellominntektsland", "ressurssvake land", "tredje verd", "fattige land", 
                "globale sør", "overgangsøkonomi", "fremvoksende økonomier", "framvoksende økonomier", "framveksande økonomi"
                "framvoksende land", "fremvoksende land", "framveksande land", "bistandsland", "minst utviklede land", "små utviklingsøystat", "små øystat",
                "kystløse utviklingsland",
                ] 
#The term "same" (NO, for Sami people) is difficult to include because of the English word "same".

phrasedefault1_5a = r'(?:{})'.format('|'.join(termlist1_5a))
phrasedefault1_5b = r'(?:{})'.format('|'.join(termlist1_5b))
phrasespecific1_5c = r'\b(?:{})\b'.format('|'.join(termlist1_5c))
phrasedefault1_5d = r'(?:{})'.format('|'.join(termlist1_5d))

```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault1_5a, na=False, case=False))
        & ((Data['result_title'].str.contains(phrasedefault1_5b, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific1_5c, na=False, case=False)))
    )
    & 
    (
        (Data['result_title'].str.contains(phrasedefault1_5d, na=False, case=False))
        |(Data['LDCSIDS']==True)
    )
),"tempsdg01_05"] = "SDG01_05"
print("Number of results = ", len(Data[(Data.tempsdg01_05 == "SDG01_05")]))  
```


```python
#Results
test=Data.loc[(Data.tempsdg01_05 == "SDG01_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 1.a

*1.a Ensure significant mobilization of resources from a variety of sources, including through enhanced development cooperation, in order to provide adequate and predictable means for developing countries, in particular least developed countries, to implement programmes and policies to end poverty in all its dimensions.*

*Sikre en betydelig mobilisering av ressurser fra ulike kilder, blant annet gjennom økt utviklingssamarbeid, for å gi utviklingslandene, særlig de minst utviklede landene, tilstrekkelige og forutsigbare midler til å gjennomføre programmer og politikk for å utrydde alle former for fattigdom*


Here a change in structure is suggested - as this is a title search, a simplification, where some terms count as relevant without needing to mention "poverty". While a work about "cooperation" would still need to mention "poverty", works are included if terms such as "official development aid" (termlist_aaalt) are in the title. We also allow just poverty to be in the title, rather than poverty alleviation specifically. 


```python
#Termlists
termlist1_aa = ["oda", "development spending", "fdi", 
                "aid", "assistance", "funding", "grant", "invest", "investment.*", "investing", "financial support", "financing", "resources", "capital flow.*",
                "cooperation", "co-operation", "collaboration.*", "network.*", "partnership.*"

                "utviklingssamarbeid.*", "utviklingsstøtte", "utviklingsstønad", "utviklingshjelp", "u-hjelp",
                "midlar", "bistand.*", "økonomiske ressurs.*", "finansiel.*", "ressurs.*", "investering", "nødhjelp", "naudhjelp",              
                "samarbeidsfond.*", "samarbeid.*", "nettverk", "partnerskap.*", "partnarskap.*"
              ]
              #Here specifying truncation because "ODA", "aid", invest" etc. need word boundaries

#Alternative option - some terms may find relevant results without using the word poverty (e.g. "development spending")?
termlist1_aaalt = ["oda", "development spending", "development assistance",
                   "bistand.*",  "utviklingssamarbeid.*", "utviklingsstøtte", "utviklingsstønad", "utviklingshjelp", "u-hjelp"
                   ]
termlist1_aaalt2 = ["fdi", "aid", "assistance", "funding", "grant", "invest", "investment.*", "investing", "financial support", "financing", "resources", "capital flow.*",
                    "cooperation", "co-operation", "collaboration.*", "network.*", "partnership.*"
                    
                    "midlar", "økonomiske ressurs.*", "finansiel.*", "ressurs.*", "investering", "nødhjelp", "naudhjelp","kapitalstrøm",              
                    "samarbeidsfond.*", "samarbeid.*", "nettverk.*", "partnerskap.*", "partnarskap.*"
                   ]

termlist1_ab = ["poverty", "pro-poor", "antipoverty",
                "fattig"
                ]

phrasespecific1_aa = r'\b(?:{})\b'.format('|'.join(termlist1_aa))
phrasespecific1_aaalt = r'\b(?:{})\b'.format('|'.join(termlist1_aaalt))
phrasespecific1_aaalt2 = r'\b(?:{})\b'.format('|'.join(termlist1_aaalt2))
phrasedefault1_ab = r'(?:{})'.format('|'.join(termlist1_ab))
```


```python
#Search 1 - within LMIC set
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasespecific1_aaalt, na=False, case=False))
        |((Data['result_title'].str.contains(phrasespecific1_aaalt2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault1_ab, na=False, case=False)))
    )
    & (Data['LMICs']==True)
    ),"tempsdg01_a"] = "SDG01_0a"

print("Number of results = ", len(Data.loc[(Data.tempsdg01_a == "SDG01_0a")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_a == "SDG01_0a"), ("result_id", "result_title")]
test.iloc[0:7, ]
```

### SDG 1.b

*1.b Create sound policy frameworks at the national, regional and international levels, based on pro-poor and gender-sensitive development strategies, to support accelerated investment in poverty eradication actions*

*Opprette gode politiske rammeverk på nasjonalt, regionalt og internasjonalt nivå basert på utviklingsstrategier som gagner de fattige og ivaretar kjønnsperspektivet, med sikte på å øke investeringer i tiltak som bekjemper fattigdom*


```python
#Termlists
termlist1_ba = ["legislat", "program", "strateg", "policy", "policies", "planning", "framework", "initiativ",
                "lovverk", "lovgiv", "politikk", "retningslinje", "utredning", "utgreiing", "rammeverk", "tiltaksplan", "planer", "planar"]
termlist1_ba_trunc = ["law", "laws", "plan", "plans"]

termlist1_bb = ["anti poverty", "anti-poverty", "antipoverty"]

termlist1_bc = ["poverty", 
                "fattig"]

termlist1_bd = ["minimi", "reduc", "mitigat", "alleviat", "tackl", "fight", "combat",
                "ending", "eliminat", "eradicat", "prevent", "out of", "overcom", "escap", "relief",

                "reduser", "bekjemp", "forhind", "nedkjemp", "motarbeid", "forebygg", "førebygg", "førebu",
                "utrydd", "kvitt", "løft", "ut av " 
                ]
termlist1_bd_trunc = ["mot", "imot", "kamp", "kampen"] #(NO)

phrasedefault1_ba = r'(?:{})'.format('|'.join(termlist1_ba))
phrasespecific1_ba_trunc = r'\b(?:{})\b'.format('|'.join(termlist1_ba_trunc))
phrasedefault1_bb = r'(?:{})'.format('|'.join(termlist1_bb))
phrasedefault1_bc = r'(?:{})'.format('|'.join(termlist1_bc))
phrasedefault1_bd = r'(?:{})'.format('|'.join(termlist1_bd))
phrasespecific1_bd_trunc = r'\b(?:{})\b'.format('|'.join(termlist1_bd_trunc))
```


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault1_ba, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific1_ba_trunc, na=False, case=False)))
    & 
    ((Data['result_title'].str.contains(phrasedefault1_bb, na=False, case=False)) 
    | (
        (Data['result_title'].str.contains(phrasedefault1_bc, na=False, case=False)) 
        & ((Data['result_title'].str.contains(phrasedefault1_bd, na=False, case=False))| (Data['result_title'].str.contains(phrasespecific1_bd_trunc, na=False, case=False)))
      )
    )
),"tempsdg01_b"] = "SDG01_b"

print("Number of results = ", len(Data[(Data.tempsdg01_b == "SDG01_b")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg01_b == "SDG01_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 1 mentions

Works mentioning SDG1.

Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 

"SDG" was also not searched for case-sensitive, as it seems to work ok without.


```python
#Termlists
#Because "SDG1" is a part of e.g. "SDG15" I prevent right hand truncation in most termlists.

termlist_sdg_a = ["SDG 1", "SDGs 1", "SDG1", "sustainable development goal 1", 
               "bærekraftsmål 1", "berekraftsmål 1"]
termlist_sdg_b = ["sustainable development goal", 
               "bærekraftsmål", "berekraftsmål"]
termlist_sdg_c = ["goal 1",
               "mål 1"]
termlist_sdg_d = ["sustainable development goal.*", "SDG", "goal 1", 
               "bærekraftsmål", "berekraftsmål", "mål 1"]
termlist_sdg_e = ["poverty",
                  "fattig"]
                  
termlist_sdg_f = ["no poverty","utrydde fattigdom"]
#Possible search for the short titles of the SDGs, to be used in a title search

phrasespecific_sdg_a = r'(?:{})\b'.format('|'.join(termlist_sdg_a))
phrasedefault_sdg_b = r'(?:{})'.format('|'.join(termlist_sdg_b))
phrasespecific_sdg_c = r'(?:{})\b'.format('|'.join(termlist_sdg_c))
phrasespecific_sdg_d = r'(?:{})\b'.format('|'.join(termlist_sdg_d))
phrasedefault_sdg_e = r'(?:{})'.format('|'.join(termlist_sdg_e))
phrasedefault_sdg_f = r'(?:{})'.format('|'.join(termlist_sdg_f))
```


```python
#Search 1
Data.loc[(
      (Data['result_title'].str.contains(phrasespecific_sdg_a, na=False, case=False))
      |(Data['result_title'].str.contains(phrasedefault_sdg_f, na=False, case=False))
      |
      (
        (Data['result_title'].str.contains(phrasedefault_sdg_b, na=False, case=False))
        & (Data['result_title'].str.contains(phrasespecific_sdg_c, na=False, case=False))
      )
      |
      (
         (Data['result_title'].str.contains(phrasespecific_sdg_d, na=False, case=False))
         & (Data['result_title'].str.contains(phrasedefault_sdg_e, na=False, case=False))
      )
    ),"tempmentionsdg01"] = "SDG01"

print("Number of results = ", len(Data[(Data.tempmentionsdg01 == "SDG01")])) 
```


```python
#Results
test=Data.loc[(Data.tempmentionsdg01 == "SDG01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 2

### SDG 2.1

*2.1 By 2030, end hunger and ensure access by all people, in particular the poor and people in vulnerable situations, including infants, to safe, nutritious and sufficient food all year round.*

*Innen 2030 utrydde sult og sikre alle mennesker, særlig fattige og personer i utsatte situasjoner, inkludert spedbarn, tilgang til nok, trygg og sunn mat hele året*

#### Phrase 1


```python
#Term lists
termlist2_1a = ["end hunger", "ending hunger", "ends hunger", "world hunger", "hunger and poverty", "poverty and hunger", "child hunger", 
                "famine", "undernourish"
                "food insecurity", "nutritional insecurity",
                
                "utrydde sult", "utrydde svolt", "utrydje svolt", "utrydda svolt", "utrydja svolt", "bekjempe sult", "bekjempe svolt", "sultne barn", "barn sult", "barnesult",
                "sult og fattigdom", "fattigdom og sult", "svolt og fattigdom", "fattigdom og svolt", "global sult", "global svolt", 
                "hungersnød", "hungersnaud", "matusikkerhet", "matmangel"
              ]

phrasedefault2_1a = r'(?:{})'.format('|'.join(termlist2_1a))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_1a, na=False, case=False))
    ),"tempsdg02_01"] = "SDG02_01"

print("Number of results = ", len(Data[(Data.tempsdg02_01 == "SDG02_01")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_01 == "SDG02_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Term lists

termlist2_1b = ["right to food", "right to adequate food", "food sovereignty",
                "nutrition security", "nutritional security", 
                "access to food", "food access", "food safety", "safe food", "food security",
                "school feeding", "free school meal", "food stamp program", "nutrition assistance", "food assistance",
                
                "tilgang til mat", "matforsyning",
                "nok mat",  "tilstrekkelig mat", "trygg mat", "mattrygghet", "sunn mat", "sunne mat", "matsikkerhet",
                "gratis skolemat", "gratis skolemåltid"
              ]
              
termlist2_1c = ["Norwegian Scientific Committee for Food Safety"]
#This term list is specific for Norway and can be dropped for works from other countries.
#There are lots of reports from VKM Norwegian Scientific Committee for Food Safety found in this string. 
#These are mostly very specialised, for example risk assessments of certain substances. Therefore removed for now, but this could be discussed.
#Note that this does not remove all VKM reports, but does exclude those with "opinion of the Norwegian Scientific Committee for Food Safety..." in the title. A number of more general reports from VKM are still there.

phrasedefault2_1b = r'(?:{})'.format('|'.join(termlist2_1b))
phrasedefault2_1c = r'(?:{})'.format('|'.join(termlist2_1c))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault2_1b, na=False, case=False))
    ) 
    & (~Data['result_title'].str.contains(phrasedefault2_1c, na=False, case=False))
),"tempsdg02_01"] = "SDG02_01"

print("Number of results = ", len(Data[(Data.tempsdg02_01 == "SDG02_01")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_01 == "SDG02_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Term lists

termlist2_1d = ["food supply"]
              #Note that this can result in some noise from biological works (e.g. food supply in a certain habitat), but it mostly gets relevant results in our dataset.

phrasedefault2_1d = r'(?:{})'.format('|'.join(termlist2_1d))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_1d, na=False, case=False))
    ),"tempsdg02_01"] = "SDG02_01"

print("Number of results = ", len(Data[(Data.tempsdg02_01 == "SDG02_01")]))   
```


```python
#Results
test=Data.loc[(Data.tempsdg02_01 == "SDG02_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 2.2

*2.2 By 2030, end all forms of malnutrition, including achieving, by 2025, the internationally agreed targets on stunting and wasting in children under 5 years of age, and address the nutritional needs of adolescent girls, pregnant and lactating women and older persons.*

*Innen 2030 utrydde alle former for feilernæring, og innen 2025 nå de internasjonalt avtalte målene som omhandler veksthemming og avmagring hos barn under fem år, og ivareta ernæringsbehovene til unge jenter, gravide, ammende kvinner og eldre personer*

#### Phrase 1


```python
#Termlists
termlist2_2a = ["malnutrition", "malnourish", "kwashiorkor", "marasmus", "anaemia", "anemia", 
                "nutritional deficien", "inadequate nutrition", "nutritional inadequa", "dietary deficien", "dietary inadequa", 
                "vitamin deficien", "inadequate vitamin", "micronutrient deficien", "inadequate micronutrient", "iron deficien", "inadequate iron", "inadequate iodine", "iodine deficien", 
                "obese", "obesity", "overweight"

                "feilernæring", "underernær", "ernæringsproblem", "jernmangel", "anemi",
                "ernæringsmangel", "kostholdsmangel", 
                "vitamin mangel", "vitaminmangel", "avitaminosis",
                "overvekt", "fedme"]

termlist2_2b = ["stunting", "stunted", "wasting", "underweight",
                "veksthemm", "avmagring", "undervekt"]

termlist2_2c = ["child", "infant", "under five", "under-five", "babies", "baby", "toddler", "girl", "boy",
                "barn", "jenter", "gutter", "gutar"]

termlist2_not = ["salmon anaemia", "salmon anemia", "lakseanemi"] 
#Norwegian specific term list for a NOT search - removed as much Norwegian research on these topics, that is not relevant to human health

phrasedefault2_2a = r'(?:{})'.format('|'.join(termlist2_2a))
phrasedefault2_2b = r'(?:{})'.format('|'.join(termlist2_2b))
phrasedefault2_2c = r'(?:{})'.format('|'.join(termlist2_2c))
phrasedefault2_2d = r'(?:{})'.format('|'.join(termlist2_not))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault2_2a, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault2_2b, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault2_2c, na=False, case=False)))
    ) 
    & (~Data['result_title'].str.contains(phrasedefault2_2d, na=False, case=False))
),"tempsdg02_02"] = "SDG02_02"

print("Number of results = ", len(Data[(Data.tempsdg02_02 == "SDG02_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_02 == "SDG02_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist2_2d = ["nutrition security", "nutritional security", "nutritional quality", "nutrition sensitive agriculture", "nutritional quality", "dietary quality",
                "safe nutrition", "access to nutrition", "reliable nutrition",

                "næringssikkerhet", "næringskvalitet", "tilgang til næring", "trygg næring"]

termlist2_2e = ["nutrition", "folate", "micronutrient",
                "ernæring", "næringsstoff", "næringsrik", "folsyre", "folacin", "folat", "mikronæring"]

termlist2_2f = ["child", "infant", "under five", "under-five", "babies", "baby", "toddler", "girl", "boy", "perinatal", "prenatal",
                "older person", "old person", "old people", "elderly", "older adult",
                "women", "mother", "pregnan",
                "school feeding", "free school meal", "food stamp program", "nutrition assistance", "food assistance",

                "barn", "jenter", "gutter", "gutar",
                "gammel person", "eldre", "de gamle",
                "kvinne", "gravid",
                "gratis skolemat", "gratis skolemåltid"]
              #We use "eldre" (NO) but not "gamle" (NO) alone because the latter is more likely to be used for non-humans (buildings etc.)

termlist2_2g = ["næringsliv", "næringsdrivend"]
#This term is an issue for Norwegian where "næring" (NO) is nutrients and "næringsliv" (NO) is business so the latter is removed with a NOT search.

phrasedefault2_2d = r'(?:{})'.format('|'.join(termlist2_2d))
phrasedefault2_2e = r'(?:{})'.format('|'.join(termlist2_2e))
phrasedefault2_2f = r'(?:{})'.format('|'.join(termlist2_2f))
phrasedefault2_2g = r'(?:{})'.format('|'.join(termlist2_2g))
```


```python
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault2_2d, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault2_2e, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault2_2f, na=False, case=False)))
    ) 
    & (~Data['result_title'].str.contains(phrasedefault2_2g, na=False, case=False))
),"tempsdg02_02"] = "SDG02_02"

print("Number of results = ", len(Data[(Data.tempsdg02_02 == "SDG02_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_02 == "SDG02_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist2_2h = ["undernutrition", "under-nutrition", "undernourish", "under-nourish", "protein deficien", "nutritional value", "nutrient content", "nutritional content",
                "underernær", "proteinmangel", "næringsinnhold", "næringsinnhald"]

phrasedefault2_2h = r'(?:{})'.format('|'.join(termlist2_2h))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_2h, na=False, case=False))
    ),"tempsdg02_02"] = "SDG02_02"

print("Number of results = ", len(Data[(Data.tempsdg02_02 == "SDG02_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_02 == "SDG02_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 2.3

*2.3 By 2030, double the agricultural productivity and incomes of small-scale food producers, in particular women, indigenous peoples, family farmers, pastoralists and fishers, including through secure and equal access to land, other productive resources and inputs, knowledge, financial services, markets and opportunities for value addition and non-farm employment.*

*Innen 2030 doble produktiviteten og inntektene til småskala matprodusenter, særlig kvinner, urfolk, familiebruk, husdyrnomader og fiskere, blant annet gjennom sikker og lik tilgang til jord, andre produksjonsressurser og innsatsmidler, kunnskap, finansielle tjenester, markeder og muligheter for verdiøkning og for sysselsetting utenfor landbruket*


```python
#Termlists
termlist2_3a = ["intensification", "production", "productivity", "yield", "output", "production resources",
                "livelihood", "income", "profit", "revenue", "economic viability", "economically viable",
                "value addition", "diversification", "non-farm employment", "off-farm employment", 
                "access", "empowerment", "benefit", "tenure", "ownership",
                "right to land", "rights to land", "land rights", "property rights", "tenure rights",
                "land grab", "tenure insecurity",
                "equity", "equitable", "justice", "injustice", "barrier", "obstacle",

                "intensivering", "produksjon", "avling", "høsting", "produksjonsressurs",
                "levebrød", "inntekt", "avkastning", "økonomi", "finansielle tjenester", "innsatsmidl",
                "verdiøkning", "verdiauke", "sysselsetting utenfor", "sysselsette utenfor", "sysselsetting utafor", "sysselsette utafor",
                "sysselsette utanfor", "sysselsetting utanfor",
                "tilgang", "myndiggjør", "fordel", "eierskap", "eigarskap",
                "landrett",  "rettigheter til land", "eiendomsrett", "eigedomsrett", "landrike", "landfattig", "jordleie",
                "likestilling", "ulikhet", "ulikskap", "rettferd", "rettighet", "ekskludering", "marginali"]
              #I have added ownership and production resources here. "tilgang/access" (NO) will cover access to land, knowledge, financial services etc.

termlist2_3b = ["smallhold", "small-hold", "small holding", "small farm", "family farm", "family-run farm", "family run farm", "family-owned farm", "family owned farm", "home gardening",
                "småbruk", "familiegård", "familiegard", "familiebruk", "kjøkkenhage", "grønnsakshage", "reindrift", "husdyrnomad"]
                #"reindrift" (NO, reindeer herding) added, often small-scale.

termlist2_3c = ["small-scale", "indigenous", "homestead", "subsistence",
                "småskal", "urfolk", "urbefolk", "sami", "sapmi", "samer", "subsistens"]
                #"Sami" was added as an indigenous group relevant for Norway. "Sami" will cover "samisk" (NO)

termlist2_3d = ["food-produc", "food produc", "grower", "agro food", "agri-food", "agro-food",
                "agricultur", "farm", "permacultur", "cropping", "orchard", "arable land",
                "pasture", "pastoral", "agroforest", "agro-forest", "silvopastur", "silvopastoral",
                "aquacultur", "maricultur", "fisher", "fish farm", "herding",
                "crop", "grain", "vegetable", "fruit", "cereal", "rice", "wheat", "maize", "pulses", "legume",
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matproduksjon", "matprodusent",
                "gård", "gard", "landbruk", "jordbruk", "gårdsbruk", "gardsbruk", "dyrket mark", "dyrkamark", "dyrka mark", "kultivert mark",
                "beite", "dyreproduksjon", "meieri",
                "fiskeoppdrett", "lakseoppdrett", "havbruk",
                "grønnsak", "grønsak", "belgfrukt", "frukt", "fisk", "laks", "sauedrift", "sauehold", " sau", "storfe", " svin", "fjærkre", " rein", "reindrift"]
                #reindeer was added as a specific species, as was salmon, to adapt to Norwegian research.

phrasedefault2_3a = r'(?:{})'.format('|'.join(termlist2_3a))
phrasedefault2_3b = r'(?:{})'.format('|'.join(termlist2_3b))
phrasedefault2_3c = r'(?:{})'.format('|'.join(termlist2_3c))
phrasedefault2_3d = r'(?:{})'.format('|'.join(termlist2_3d))

```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_3a, na=False, case=False)) 
    & 
    (
        (Data['result_title'].str.contains(phrasedefault2_3b, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault2_3c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault2_3d, na=False, case=False)))
    )
    ),"tempsdg02_03"] = "SDG02_03"

print("Number of results = ", len(Data[(Data.tempsdg02_03 == "SDG02_03")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_03 == "SDG02_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 2.4

*2.4 By 2030, ensure sustainable food production systems and implement resilient agricultural practices that increase productivity and production, that help maintain ecosystems, that strengthen capacity for adaptation to climate change, extreme weather, drought, flooding and other disasters and that progressively improve land and soil quality.*

*Innen 2030 sikre at det fSDG02_04innes bærekraftige systemer for matproduksjon, og innføre robuste metoder som gir økt produktivitet og produksjon, som bidrar til å opprettholde økosystemene, som styrker evnen til tilpasning til klimaendringer, ekstremvær, tørke, oversvømmelse og andre katastrofer, og som gradvis bedrer arealenes og jordas kvalitet*

#### Phrase 1


```python
#Termlists
termlist2_4a = ["food-produc", "food produc", "grower", "agrifood", "agri-food", "agro-food", "agro food",
                "agricultur", "farm", "smallhold", "small-hold", "permacultur", "cropping", "orchard", "arable land",
                "pasture", "pastoral", "agroforest", "agro-forest", "silvopastur", "silvopastoral",
                "aquacultur", "maricultur", "fisher", "fish farm", "herding",
                "crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", "legume",
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                "fodder", "animal feed ", "fish feed ",
                
                "matproduksjon", "matprodusent",
                "gård", "gard", "landbruk", "jordbruk", "gårdsbruk", "gardsbruk", "småbruk", "familiebruk", "dyrket mark", "dyrkamark",
                "dyrka mark", "kultivert mark",
                "beite", "dyreproduksjon", "meieri",
                "fiskeoppdrett", "lakseoppdrett", "havbruk",
                "grønnsak", "grønsak", "belgfrukt", "frukt", "fiske", "laks", " sau ", "sauedrift", "sauehold", "storfe", " svin", "fjærkre", " rein",
                "bærekraftig fôr", "berekraftig fôr", "dyrefôr", "dyrefor ", "fiskefôr", "fiskefor "]
                #Space before " rice" to avoid "price", similarly "sau/svin" (NO) and after "xxxfor" (NO, to avoid "forbund" etc.). Note that "agricultur" will also cover e.g. "ecoagriculture"
    
termlist2_4b = ["intensif", "productivity", "efficiency", "yield", "agricultural output", "farm output",
                "produktivitet", "effektivitet", "avling"]

termlist2_4c = ["production", "produksjon"]

termlist2_4d = ["increas", "improv",
                "økt", "øke", "auke", "auka"]
                #"production" is combined with "increasing" because a lot of the results were too irrelevant when alone.

phrasedefault2_4a = r'(?:{})'.format('|'.join(termlist2_4a))
phrasedefault2_4b = r'(?:{})'.format('|'.join(termlist2_4b))
phrasedefault2_4c = r'(?:{})'.format('|'.join(termlist2_4c))
phrasedefault2_4d = r'(?:{})'.format('|'.join(termlist2_4d))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_4a, na=False, case=False)) 
    & (
        (Data['result_title'].str.contains(phrasedefault2_4b, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault2_4c, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault2_4d, na=False, case=False)))
      )
    ),"tempsdg02_04"] = "SDG02_04"

print("Number of results = ", len(Data[(Data.tempsdg02_04 == "SDG02_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_04 == "SDG02_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist2_4e = ["climate smart", "climate-smart", "resilien", "vulnerability", 
                "risk reduction", "disaster reduction",
                "disaster plan", "disaster management", "disaster strateg", "disaster relief", "disaster program", "risk plan", "risk management", "risk strate", "manage risk", "risk program",
                
                "klimasmart", "sårbar",
                "risikoplan", "katastrofe", "beredskap"
                ]
                #It was necessary to have disasters and plans in phrases in english because there are a lot of results about 
                #e.g. risks to local habitats from agriculture, rather than risks to agriculture


phrasedefault2_4e = r'(?:{})'.format('|'.join(termlist2_4e))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_4a, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault2_4e, na=False, case=False))
    ),"tempsdg02_04"] = "SDG02_04"

print("Number of results = ", len(Data[(Data.tempsdg02_04 == "SDG02_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_04 == "SDG02_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist2_4f = ["adapt", "mitigat", "protect", "avoid", "limit", "prevent", "manag", 
                "planning", "plans", "strateg", "disaster reduc", "risk reduc", "relief", "program", "programme", "policy", "policies", "strateg", "framework", "governance", "legislat",
                "cope", "coping", "tolera", "preparedness", "early warning",
                "sendai",

                "tilpass", "forbered", "førebu", "beskytt", "unngå", "begrens", "hindr", "forebygg", "førebygg" ,"håndter",
                "planer", "planlegging", "handlingsplan", "rammeverk", "politikk", "retningslin", "styring", "ledelse", "leiing", "lovgiv", 
                "katastrofeplanlegging", "risikoreduksjon", "strategi", "krisehåndtering", "tåle", "beredskap", "varsling", "varsel"]
              
termlist2_4g = ["climate change", "changing climate", "global warming",
                "disaster", "catastrophe", "hazard",
                "extreme climat", "extreme weather", "extreme precipitation", "extreme rain", "extreme snow", "extreme temperatur", "extreme storm", "extreme wind", 
                 "rogue wave", "tsunami", "cyclone", "typhoon", "hurricane", "tornado", 
                 "drought", "flood", 
                 "avalanche", "landslide", "land-slide", "land slide", "rockslide", "rock-slide", "rock slide", "rockfall", "surface collapse", "mudflow", "mud-flow", 
                 "cold spell", "cold wave", "dzud", "blizzard", "snowstorm", 
                 "heatwave", "heat-wave", 
                 "earthquake", "volcan", "ash cloud", "ash fall", "tephra", 
                 "wildfire", "wild-fire", "wild fire", "forest-fire", "forest fire", "forestfire", 
                 "sea-level rise", "sea-level change", "rising sea-level", 
                 "outbreak", "pandemic", "epidemic", 
                 "armed conflict", "political instability", "civil instability", "politically volatile", 
                 "unrest", "financial crash", "financial shock", "economic downturn", "economic shock",
                
                "klimaendring", "global oppvarm", 
                "katastrof", "krise", 
                 "ekstremvær", "ekstremver", 
                 "tropisk lavtrykk", "tropisk lågtrykk", "flodbølg", "monsterbølg", "ekstrembølg", 
                 "orkan",  "tyfon", "syklon", "snøstorm", 
                 "flom", "flaum", "oversvøm", "ovefløym", "tørke", 
                 "snøskred", "skred", "snøras", "lavine", "jordskred", "jordras", "sørpeskred", "leirras", "leirskred", "steinras", "steinskred", "synkehull", 
                 "uvanlig kulde", "uvanlig kaldt", "uvanleg kulde", "uvanleg kaldt", "ekstrem kuld", "ekstremkuld", "kuldebølg", "snøstorm", 
                 "varmebølg", "hetebølg", "ekstrem varm", "ekstremvarm", "uvanlig varm", "uvanleg varm", 
                 "jordskjelv", "vulkan", "askenedfall", "oskenedfall", "askesky", "oskesky", 
                 "skogbrann", "gressbrann", "grasbrann", "lyngbrann", 
                 "havnivåstigning", "stormflo", 
                 "pandemi", "epidemi", "utbrudd", "utbrot",
                 "politisk ustabilitet", "væpnede konflikter", "væpnet konflikt", "væpna konflikt", "borgerkrig", "borgarkrig", "fremmedkrig", "finanskrise", "finanssjokk", 
                 "finanskatastrofe", "finanskræsj", "økonomisk nedgang", "økonomisk sjokk", "økonomisk katastrofe"]

termlist2_4h = ["war", "wars", 
                "krig", "ras"]  

phrasedefault2_4f = r'(?:{})'.format('|'.join(termlist2_4f))
phrasedefault2_4g = r'(?:{})'.format('|'.join(termlist2_4g))
phrasespecific2_4h = r'\b(?:{})\b'.format('|'.join(termlist2_4h))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_4a, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault2_4f, na=False, case=False))
    & ((Data['result_title'].str.contains(phrasedefault2_4g, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific2_4h, na=False, case=False)))
    ),"tempsdg02_04"] = "SDG02_04"

print("Number of results = ", len(Data[(Data.tempsdg02_04 == "SDG02_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_04 == "SDG02_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4
The following report from NIBIO was used to help with Norwegian sustainable agriculture terms: Bøe et al. (2020) Fangvekster som klimatiltak i Norge. Egnet dyrkingsareal, potensiale for klimagassbesparelse, kostnader, barrierer og virkemiddel. NIBIO Report. http://hdl.handle.net/11250/2638984



```python
#Termlists
termlist2_4i = ["ecoagricultur", "eco-agricultur", "agroecolog", "permaculture", "conservation agriculture", "conservation farming",
                "organic farm", "organic agricult", "organic crop", "organic orchard", "organic arable", "organic pasture",
                "organic aquacultur", "organic salmon", "organic pig", "organic poultry", "organic dairy", "organic reindeer",

                "økolandbruk", "økojordbruk", "permakultur"     
                ]
                #"organic" is not used alone, but is instead combined in phrases to avoid e.g. organic acids, organic matter. Moved to this part rather than 4j as it can stand alone.
                #"bærekraftig fôr" (NO) is added specifically due to it's inclusion as a priority area ("samfunnsoppdrag") in the governments Long-term plan.
              
termlist2_4j = ["sustainab", "eco-friendly", "environmentally friendly", "ecosystem approach", "ecosystem based",
                "natural pest control", "natural pest management", "biological pest control", "intergrated pest management",
                "intercropping", "cover crop", "crop rotation", "polyculture", "permaculture", 
                "reduced tillage", "mulch", "mulching",
                "water conservation",

                "bærekraftig", "berekraftig", "selvbærende", "sjølvberande", "miljøvennlig", "miljøvennleg", "miljøvenleg", "miljøbevisst", "miljømedveten", "miljømedviten", "økosystem", 
                "økologisk", "biologisk bekjempelse", "biologisk nedkjemping", "biologisk skadedyrkontroll", "integrert skadedyrkontroll", "integrert ugrasbekjempelse", "integrert plantevern",
                "vekstskifte", "grønngjødsling", "dekkvekst", "underkultur", "underså", "ettervekster", "polykultur", "permakultur",
                "redusert jordarbeiding", "gjødselplanlegging",
                "vannsparing"                
                ] 

phrasedefault2_4i = r'(?:{})'.format('|'.join(termlist2_4i))
phrasedefault2_4j = r'(?:{})'.format('|'.join(termlist2_4j))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_4i, na=False, case=False)) 
    | ((Data['result_title'].str.contains(phrasedefault2_4a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault2_4j, na=False, case=False)))
    ),"tempsdg02_04"] = "SDG02_04"

print("Number of results = ", len(Data[(Data.tempsdg02_04 == "SDG02_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_04 == "SDG02_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 5
The following NIBIO report was used to help with relevant Norwegian terms around soil management: Bardalen et al. (2021). Jordvernets begrunnelser Kunnskapsgrunnlag for revidert jordvernstrategi. NIBIO Report. https://hdl.handle.net/11250/2738064


```python
#Termlists
termlist2_4k = ["soil conserv", "soil structure", "soil fertility", "soil health", "soil improvement",
                "soil quality", "land quality", "farmland quality", "quality of soil", "quality of land",
                "biodiversit", "species diversity", "ecosystem", "pollinator",

                "jordvern", "jordfunksjon", "jordforbedring", "jordforbetring", "jordforvaltning", "jordkvalitet", "jordas kvalitet",
                "biologisk mangfold", "biologiske mangfold", "biologisk mangfald", "biomangfold", "biomangfald", "artsmangfold", "artsmangfald",
                "naturmangfold", "naturmangfald", "økosystem"
                ]

phrasedefault2_4k = r'(?:{})'.format('|'.join(termlist2_4k))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_4a, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault2_4k, na=False, case=False))
    ),"tempsdg02_04"] = "SDG02_04"

print("Number of results = ", len(Data[(Data.tempsdg02_04 == "SDG02_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_04 == "SDG02_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 6
The following NIBIO report was used to help with relevant Norwegian terms around soil management: Bardalen et al. (2021). Jordvernets begrunnelser Kunnskapsgrunnlag for revidert jordvernstrategi. NIBIO Report. https://hdl.handle.net/11250/2738064


```python
#Termlists
#Note that we don't need biodiversity/pollinator terms here because they are already covered in phrase 5
termlist2_4l = ["desertification", "land degradation", "environmental impact", "environmental footprint",
                "vannknapphet", "ørkenspredning", "ørkenspreiing", "forørkning", "landforringelse", "jordforringelse", "miljøpåvirk", "fotavtrykk"]

termlist2_4m = ["soil", "cropland", "farmland", "arable land", "cultivated land", "agricultural land",
                "jord", "dyrket mark", "dyrka mark", "dyrkamark", "dyrket land", "dyrka land"]
                #"land" had some noise if used alone, for example "Greenland"

termlist2_4n = ["loss", "degradation", "depletion", "erosion", "compaction", "waterlogging", "salinization", "salinisation", "acidifi", "pollut", "contaminat", "vulnerab",
                "forring", "forverr", "næringsfattig", "avrenning", "jordtap", "erosjon", "forsalting", "jordpakking", "forsuring", "forurensing", "forureining", "sårbar"]

phrasedefault2_4l = r'(?:{})'.format('|'.join(termlist2_4l))
phrasedefault2_4m = r'(?:{})'.format('|'.join(termlist2_4m))
phrasedefault2_4n = r'(?:{})'.format('|'.join(termlist2_4n))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_4a, na=False, case=False)) 
    & 
      ((Data['result_title'].str.contains(phrasedefault2_4l, na=False, case=False))
      | ((Data['result_title'].str.contains(phrasedefault2_4m, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault2_4n, na=False, case=False)))
      )
    ),"tempsdg02_04"] = "SDG02_04"

print("Number of results = ", len(Data[(Data.tempsdg02_04 == "SDG02_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_04 == "SDG02_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 2.5

*2.5 By 2020, maintain the genetic diversity of seeds, cultivated plants and farmed and domesticated animals and their related wild species, including through soundly managed and diversified seed and plant banks at the national, regional and international levels, and promote access to and fair and equitable sharing of benefits arising from the utilization of genetic resources and associated traditional knowledge, as internationally agreed.*

*Innen 2020 opprettholde det genetiske mangfoldet av frø, kulturplanter, husdyr og beslektede ville arter, blant annet gjennom veldrevne og rikholdige frø- og plantesamlinger nasjonalt, regionalt og internasjonalt, og fremme tilgang til og en rettferdig og likeverdig fordeling av de goder som følger av bruk av genressurser og tilhørende tradisjonell kunnskap, i tråd med internasjonal enighet*

#### Phrase 1 & 2
These two are combined here because it was difficult to find completely non-overlapping terms in Norwegian. Phrase 1 deals with terms quite specific to animal and plant genetic diversity in agriculture, while phrase 2 deals with genetic resources generally combined with agriculture. In practice, here the approach for these became so similar that I combined them. 


```python
#Termlists
termlist2_5a = ["plant genetic resource", "animal genetic resource", 
                "agricultural diversity", "agricultural biodiversity", "agrobiodiversity",
                "wild relative", 
                "local breed", "local cultivar", "traditional breed", "traditional cultivar", "indiengous breed", "indigenous cultivar", "autochthonous breed", "autochthonous cultivar",
                "indigenous variet", "indigenous crop", "indigenous grain", "indigenous vegetable", "indigenous fruit", "indigenous cereal", "indigenous rice", "indigenous wheat", "indigenous maize", "indigenous pulse",
                "indigenous livestock", "indigenous poultry", "indigenous cattle", "indigenous sheep", "indigenous goat", "indigenous chicken", "indigenous duck", "indigenous buffalo",
                "traditional livestock", "traditional poultry", "traditional cattle", "traditional sheep", "traditional goat", "traditional chicken", "traditional duck", "traditional buffalo",
                "traditional variet", "traditional crop", "traditional grain", "traditional vegetable", "traditional fruit", "traditional cereal", "traditional rice", "traditional wheat", "traditional maize", "traditional pulse",
                "local variet", "local crop", "local grain", "local vegetable", "local fruit", "local cereal", "local rice", "local wheat", "local maize", "local pulse",
                "local livestock", "local poultry", "local cattle", "local sheep", "local goat", "local chicken", "local duck", "local buffalo",
                "landrace",
                
                "plantegenetiske ressurs", "dyrgenetiske ressurs", "dyregenetiske ressurs",
                "biologisk mangfold for mat","biologisk mangfold for landbruk","biologisk mangfold for jordbruk",
                "biologisk diversitet for mat","biologisk diversitet for landbruk","biologisk diversitet for jordbruk",
                "biomangfold for mat","biomangfold for landbruk","biomangfold for jordbruk",
                "ville slekt", "villslekt",
                "gamle eplesort", "gamle eplevariant", "tradisjonelle eplesort", "tradisjonelle eplevariant"]
                #Apples are added in Norwegian as this seems to be a specific focus area

termlist2_5b = ["heirloom", "wild relative", "genetic resource", "genetic diversity",
                "mangfold", "mangfald", "ville", "viltvoks", "viltvaks", "tradisjonelle", "genetiske ressurs", "genressurs", "genetikk diversit"]

termlist2_5c = ["food-produc", "food produc", "grower", "agrifood", "agri-food", "agro-food", "agro food",
                "agricultur", "farm", "smallhold", "small-hold", "permacultur", "cropping", "orchard", "arable land",
                "pasture", "pastoral", "agroforest", "agro-forest", "silvopastur", "silvopastoral",
                "aquacultur", "maricultur", "fisher", "fish farm", "herding",
                "crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", "legume",
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matproduksjon", "matprodusent",
                "landbruk", "jordbruk", "gårdsbruk", "gardsbruk", "småbruk", "familiebruk", "dyrket mark", "dyrkamark", "dyrka mark", "kultivert mark",
                "beite", "dyreproduksjon", "meieri",
                "fiskeoppdrett", "lakseoppdrett", "havbruk",
                "grønnsak", "grønsak", "frukt", "laks", " sau", "storfe", " svin", "fjærkre", " rein",
                "eplesort", "epler", "epledyrk"]
                #"husdyr" (NO) was tested but mostly brought noise about household fauna
                #"gård" (NO) was also removed as mostly were results with place names (e.g Oppegård)
                #"fish" is changed to "fisher" here to avoid fish diversity works
                #"eple" (NO) is used in other forms because it is a part of other words such as "sykEPLEier".

phrasedefault2_5a = r'(?:{})'.format('|'.join(termlist2_5a))
phrasedefault2_5b = r'(?:{})'.format('|'.join(termlist2_5b))
phrasedefault2_5c = r'(?:{})'.format('|'.join(termlist2_5c))
```


```python
#Search 1
Data.loc[(
   (Data['result_title'].str.contains(phrasedefault2_5a, na=False, case=False)) 
    | (
        (Data['result_title'].str.contains(phrasedefault2_5b, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault2_5c, na=False, case=False))
      )
    ),"tempsdg02_05"] = "SDG02_05"

print("Number of results = ", len(Data[(Data.tempsdg02_05 == "SDG02_05")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_05 == "SDG02_05"), ("result_id", "result_title")]
test.iloc[20:30, ]
```

#### Phrase 3

Here we have simplified (to adapt from abstract to title search) - drop the terms starting `"diversity" OR "genetic resources"...` so it is enough for the title to mention cryoconservation / genebanks. In the abstract the more detialed approach was necessary becaue many works mention that they *used* a gene bank in the methods, but are not about gene banks. 


```python
#Termlists
termlist2_5d = ["cryoconserv", 
                "kryo-bevaring", "kryobevaring"] 

termlist2_5e = ["plant bank", "seed bank", "genebank", "germplasm bank", "cryobank", "ex-situ", "cryopreserv", 
                "frøhvelv", "frøkvelv", "plantebank", "frøbank", "genbank", "genbevaring", "genressurssenter", "kimplasmabank", "kimplasmabevaring", "kryopreserv"]

phrasedefault2_5d = r'(?:{})'.format('|'.join(termlist2_5d))
phrasedefault2_5e = r'(?:{})'.format('|'.join(termlist2_5e))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_5c, na=False, case=False)) 
    & ((Data['result_title'].str.contains(phrasedefault2_5d, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault2_5e, na=False, case=False)))
    ),"tempsdg02_05"] = "SDG02_05"

print("Number of results = ", len(Data[(Data.tempsdg02_05 == "SDG02_05")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_05 == "SDG02_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4 & 5


```python
#Termlists
termlist2_5f = ["genetic resource", "agrobiodiversity",
                "plant bank", "seed bank", "genebank", "germplasm bank", "cryobank", "ex-situ", "cryopreserv", 
                "seed commons",
                "bioprospect", 
                "traditional knowledge", "local knowledge", "indigenous knowledge","autochthonous knowledge", 
                
                "genetiske ressurs", "genressurs", 
                "frøhvelv", "frøkvelv","plantebank", "frøbank", "genbank", "genbevaring", "kimplasmabevaring", "kimplasmabank", "kimplasmaressurs",  "kryopreserv",
                "frøallmenning",
                "bioprospekt",
                "tradisjonelle kunnskap", "tradisjonell kunnskap", "urfolkskunnskap", "urfolksperspektiv"]
              
termlist2_5g = ["governance", "justice", "ownership",
                "biopira", "inequit", 
                "material transfer", "consent", "sharing", "equitab", "equal", "fair", "access", "right", "availab",
                "Convention on biological diversity", "CBD", "Nagoya", 

                "myndig", "styring", "ledelse", "leiing", "rettferd", "eierskap", "eigarskap",
                "avtale", "deling", "deler", "tilgang", "tilgjeng", "rett",
                "Konvensjonen om biologisk mangfold"] 

termlist2_5h = ["International Seed Treaty", "Global Plan of Action for Animal Genetic Resources", "Plant Genetic Resources for Food and Agriculture", "PGRFA",
                "Den internasjonale plantetraktaten"]

phrasedefault2_5f = r'(?:{})'.format('|'.join(termlist2_5f))
phrasedefault2_5g = r'(?:{})'.format('|'.join(termlist2_5g))
phrasedefault2_5h = r'(?:{})'.format('|'.join(termlist2_5h))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault2_5c, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault2_5f, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault2_5g, na=False, case=False))
    )
    |(Data['result_title'].str.contains(phrasedefault2_5h, na=False, case=False))
    ),"tempsdg02_05"] = "SDG02_05"

print("Number of results = ", len(Data[(Data.tempsdg02_05 == "SDG02_05")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_05 == "SDG02_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 2.a

*2.a Increase investment, including through enhanced international cooperation, in rural infrastructure, agricultural research and extension services, technology development and plant and livestock gene banks in order to enhance agricultural productive capacity in developing countries, in particular least developed countries.*

*Blant annet gjennom bedre internasjonalt samarbeid øke investeringene i infrastruktur på landsbygda, i forskning og veiledningstjenester innenfor landbruket, i teknologiutvikling og i genbanker for planter og husdyr, med sikte på å forbedre produksjonskapasiteten i landbruket i utviklingsland, særlig i de minst utviklede landene*


```python
#Termlists
termlist2_aa = ["Agriculture Orientation Index for Government Expenditure"]

termlist2_ab = ["government expenditure", "government spending", "public expenditure", "public spending",
                "investment", "investing", "invest ", "finance", "financing", "fund", "grant", "financial resource",
                "cooperation fund", "co-operation fund", "development spending", 
                "international cooperation", "international co-operation", "international collaboration", "international network", "international partnership", "international aid", "international assistance",
                "international development", "development cooperation", "development co-operation", "development collaboration", "development network", "development partnership", "development aid", "development assistance",
                "foreign cooperation", "foreign co-operation", "foreign collaboration", "foreign network", "foreign partnership", "foreign aid", "foreign assistance",

                "statsbudsjett", "statsstøtte", "offentlig støtte", 
                "finansiel", "midlar", "økonomiske ressurs",
                "samarbeidsfond", "utviklingsstøtte", "utviklingsstønad", "bistand", "utviklingshjelp", "u-hjelp",
                "utviklingssamarbeid", "internasjonalt samarbeid", "internasjonale samarbeid"]

termlist2_ab_trunc = ["ODA"]

termlist2_ac = ["rural infrastructure", "rural infrastructure", "rural techn", "rural development",
                "agronom", "agroecolog", "agro-ecolog", "agricultural sector",
                "plant bank", "seed bank", "gene bank", "genebank", "germplasm bank", "cryobank",
                "agricultur", "farm", "smallhold", "small-hold", "irrigat", "agrofood", "agrifood", "agri food", "agri-food", "aquacultur", "maricultur",

                "frøhvelv", "frøkvelv", "plantebank", "frøbank", "genbank", "genbevaring", "genressurssenter", "kimplasmabank", "kimplasmabevaring",
                "jordbruk", "landbruk", "gård", "gard", "småbruk", "familiebruk", "matprodusent", "matproduksjon", "akvakultur", "havbruk"]

phrasedefault2_aa = r'(?:{})'.format('|'.join(termlist2_aa))
phrasedefault2_ab = r'(?:{})'.format('|'.join(termlist2_ab))
phrasespecific2_ab = r'\b(?:{})\b'.format('|'.join(termlist2_ab_trunc))
phrasedefault2_ac = r'(?:{})'.format('|'.join(termlist2_ac))
```


```python
#Search - in LMICs
Data.loc[(
    (
      (Data['result_title'].str.contains(phrasedefault2_aa, na=False, case=False)) 
      |
        (
            ((Data['result_title'].str.contains(phrasedefault2_ab, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific2_ab, na=False, case=False)))
            & (Data['result_title'].str.contains(phrasedefault2_ac, na=False, case=False)) 
        )
    )
    & (Data['LMICs']==True)
),"tempsdg02_a"] = "SDG02_0a"

print("Number of results = ", len(Data[(Data.tempsdg02_a == "SDG02_0a")]))  
```


```python
#Results
test=Data.loc[(Data.tempsdg02_a == "SDG02_0a"), ("result_id", "result_title")]
test.iloc[0:15, ]
```

### SDG 2.b

*2.b Correct and prevent trade restrictions and distortions in world agricultural markets, including through the parallel elimination of all forms of agricultural export subsidies and all export measures with equivalent effect, in accordance with the mandate of the Doha Development Round.*

*Korrigere og hindre handelsrestriksjoner og vridninger på verdens landbruksmarkeder, blant annet gjennom en parallell avvikling av alle former for eksportsubsidier på landbruksvarer og alle eksporttiltak med tilsvarende effekt, i samsvar med mandatet for Doha-runden*


```python
#Termlists
termlist2_ba = ["export subsid","export credit","export financ","export competition","export support",
                "eksportsubsidi", "eksporttiltak", "eksportrestriksjon", "markeds-forstyrrende",]

termlist2_bb = ["food", "agricultur", "aquacult", "maricult", 
                "crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", "legume", 
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matprod", "gård", "landbruk", "jordbruk", "fiskeoppdrett", "lakseoppdrett", "havbruk", "akvakultur",
                "grønnsak", "grønsak", "frukt", "fisk", "laks", " sau", "storfe", " svin", "fjærkre", "rein"]

termlist2_bc = ["distort", "price-fixing", "dumping", "trade restrict", "sanction", "Doha", "food aid", "state support","state financial support",
                "WTO dispute",

                "vridning", "handelsrestriksjon", "matbistand", 
                "verdens handelsorganisasjon", "verdas handelsorganisasjon", "handelsreform"]

#termlist2_bd = ["trade", "trading", "market", "export", "import",       
#                "handel", "marked", "marknad", "eksport"]

phrasedefault2_ba = r'(?:{})'.format('|'.join(termlist2_ba))
phrasedefault2_bb = r'(?:{})'.format('|'.join(termlist2_bb))
phrasedefault2_bc = r'(?:{})'.format('|'.join(termlist2_bc))
#phrasedefault2_bd = r'(?:{})'.format('|'.join(termlist2_bd))
```


```python
#Search 1
#Note that although the WOS phrase would be a&b|b&c&d, here in the title search d is not as necessary. Removing it adds 1 more result.

Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_bb, na=False, case=False)) 
    & 
    (
        (Data['result_title'].str.contains(phrasedefault2_ba, na=False, case=False))
        |(Data['result_title'].str.contains(phrasedefault2_bc, na=False, case=False))
    )
    ),"tempsdg02_b"] = "SDG02_b"

print("Number of results = ", len(Data[(Data.tempsdg02_b == "SDG02_b")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_b == "SDG02_b"), ("result_id", "result_title")]
test.iloc[0:6, ]
```

### SDG 2.c

*2.c Adopt measures to ensure the proper functioning of food commodity markets and their derivatives and facilitate timely access to market information, including on food reserves, in order to help limit extreme food price volatility.*

*Vedta tiltak for å sikre at råvare- og derivatmarkedene for matvarer er velfungerende og legge til rette for rask tilgang til markedsinformasjon, blant annet om matreserver, for å begrense ekstreme svingninger i matvareprisene*


```python
#Termlists
termlist2_ca = ["food", "agricultur", "aquacultur", "maricultur",
                " crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", "legume",
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matprod", "gård", "gard", "landbruk", "jordbruk",
                "fiskeoppdrett", "lakseoppdrett", "havbruk", "akvakultur", 
                "grønnsak", "grønsak", "frukt", "fisk", "laks", " sau", "storfe", "svine", "fjærkre", "rein"]
                #"food" will find agrifood etc.
                #I've added a space before "crop" and "rice" to prevent "macro" and "price"
                #using "svine"(NO) here instead of svin, because we expect it to talk about svineprodukt, but also because it only adds 1 noisy result

termlist2_cb = ["price", "market", "trade", "trading",
                "pris", "kostnad", "marked", "marknad", "verdenshandel", "verdshandel", "internasjonal handel", "internasjonale handel"]

termlist2_cc = ["volatil","anomalies","price shock","price spike","inflation","stabil","stable","function",
                "sving", "forutsig", "forutsei", "prishopp","prissjokk","inflasjon","funksjon"]
                #"stabil" will find stabilis/ze, stability, instability, and the Norwegian term for stable/unstable (stabil, NO). 
                #"Volatil" will find the Norwegian word too.

termlist2_cd = ["price", 
                "pris", "kostnad"]

termlist2_ce = ["market", "marknad", "trading", "trading", 
                "marked", "verdenshandel", "verdshandel", "internasjonal handel", "internasjonale handel"]

phrasedefault2_ca = r'(?:{})'.format('|'.join(termlist2_ca))
phrasedefault2_cb = r'(?:{})'.format('|'.join(termlist2_cb))
phrasedefault2_cc = r'(?:{})'.format('|'.join(termlist2_cc))
phrasedefault2_cd = r'(?:{})'.format('|'.join(termlist2_cd))
phrasedefault2_ce = r'(?:{})'.format('|'.join(termlist2_ce))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault2_ca, na=False, case=False)) 
    & 
    (
        ((Data['result_title'].str.contains(phrasedefault2_cb, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault2_cc, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault2_cd, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault2_ce, na=False, case=False)))
    )
    ),"tempsdg02_c"] = "SDG02_c"

print("Number of results = ", len(Data[(Data.tempsdg02_c == "SDG02_c")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_c == "SDG02_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 2 mentions

Works mentioning the SDG


```python
#Termlists
termlist_sdg_a = ["SDG 2", "SDGs 2", "SDG2", "sustainable development goal 2", 
                  "bærekraftsmål 2"]
termlist_sdg_b = ["sustainable development goal", 
                  "bærekraftsmål"]
termlist_sdg_c = ["goal 2",
                  "mål 2"]
termlist_sdg_d = ["sustainable development goal.*", "SDG", "goal 2", 
                  "bærekraftsmål.*", "mål 2"]
termlist_sdg_e = ["hunger", "food", 
                  "utrydde sult"]

phrasespecific_sdg_a = r'(?:{})\b'.format('|'.join(termlist_sdg_a))
phrasedefault_sdg_b = r'(?:{})'.format('|'.join(termlist_sdg_b))
phrasedefault_sdg_c = r'(?:{})'.format('|'.join(termlist_sdg_c))
phrasespecific_sdg_d = r'(?:{})\b'.format('|'.join(termlist_sdg_d))
phrasedefault_sdg_e = r'(?:{})'.format('|'.join(termlist_sdg_e))
```

Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 

"SDG" was also not searched for case-sensitive, as it seems to work ok without.

Right truncation on SDG2 is prevented to avoid the course code SDG214 (Norway-specific problem). 


```python
#Search 1
Data.loc[(
      (Data['result_title'].str.contains(phrasespecific_sdg_a, na=False, case=False))
      |((Data['result_title'].str.contains(phrasedefault_sdg_b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault_sdg_c, na=False, case=False)))
      |((Data['result_title'].str.contains(phrasespecific_sdg_d, na=False, case=False))& (Data['result_title'].str.contains(phrasedefault_sdg_e, na=False, case=False)))
    ),"tempmentionsdg02"] = "SDG02"

print("Number of results = ", len(Data[(Data.tempmentionsdg02 == "SDG02")])) 
```


```python
test=Data.loc[(Data.tempmentionsdg02 == "SDG02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 3

To help with sourcing Norwegian terms, we used webpages about SDG targets from the UN Association of Norway (https://www.fn.no/om-fn/fns-baerekraftsmaal/god-helse-og-livskvalitet) and  "Realfagstermer", a controlled vocabulary for scientific terms from the University of Oslo and University of Bergen (https://app.uio.no/ub/emnesok/realfagstermer/search).

### SDG 3.1

*By 2030, reduce the global maternal mortality ratio to less than 70 per 100,000 live births.*

*Innen 2030 redusere mødredødeligheten i verden til under 70 per 100 000 levendefødte*


Because this is a title search, it is less important with the NOT search implemented in the WoS strings (it does not seem to cause as much noise). It may be more important for use on research sets which have large amounts of agricultural research. 


```python
#Termlists
termlist3_1a = ["pregnan","post partum","postpartum","peripartum","obstetric",
                "premature deliver","preterm deliver","preterm labor","preterm labour","childbirth",
                "maternal","mothers",

                "gravid", "obstetrikk",
                "mødre"]

termlist3_1atrunk = ["mor"]

termlist3_1b = ["mortality","death",
                "død"] 

termlist3_1c = ["mødredødelighet"]

phrasedefault3_1a = r'(?:{})'.format('|'.join(termlist3_1a))
phrasedefault3_1b = r'(?:{})'.format('|'.join(termlist3_1b))
phrasedefault3_1c = r'(?:{})'.format('|'.join(termlist3_1c))
phrasedefault3_1atrunk = r'\b(?:{})\b'.format('|'.join(termlist3_1atrunk))

#This string is hard to create in a way that cleanly separates out results about mortality for children/babies, which should be in 3.2
#"birth" in particular seems to be an issue and is removed from this string; it is included in 3.2, and here as "childbirth"
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_1c, na=False, case=False))
    |
    (
        ((Data['result_title'].str.contains(phrasedefault3_1a, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault3_1atrunk, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault3_1b, na=False, case=False)) 
    )
    ),"tempsdg03_01"] = "SDG03_01"

print("Number of results = ", len(Data[(Data.tempsdg03_01 == "SDG03_01")])) 
```


```python
test=Data.loc[(Data.tempsdg03_01 == "SDG03_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.2

*By 2030, end preventable deaths of newborns and children under 5 years of age, with all countries aiming to reduce neonatal mortality to at least as low as 12 per 1,000 live births and under‑5 mortality to at least as low as 25 per 1,000 live births*

*Innen 2030 få slutt på dødsfall som kan forhindres blant nyfødte og barn under fem år, med et felles mål for alle land om å redusere dødeligheten blant nyfødte til høyst 12 per 1 000 levendefødte og til høyst 25 per 1 000 levendefødte blant barn under fem år*

Phrases 1 and 2 are combined here.


```python
#Termlists
termlist3_2a = ["child","infant","toddler","under-five",
                "baby","babies","newborn","neonatal","neonate","birth",
                "perinatal","prenatal","antenatal",

                "barn", "under 5 år", "under fem år",
                "nyfød", "spedbarn", "føds", "for tidlig født"
              ]
              #"føds" (NO) is used to capture both "fødsel" and  "fødsler" etc.
              #In Norwegian, "for tidlig født" (NO) can be used for premature babies. It is not included in english specifically because
              #it would be strange not to include the words "baby", "newborn" etc. together with premature (?).

termlist3_2b = ["mortality","death","stillbirth","still-birth", "surviv",
                "mortalitet", "død", "overleve"]

phrasedefault3_2a = r'(?:{})'.format('|'.join(termlist3_2a))
phrasedefault3_2b = r'(?:{})'.format('|'.join(termlist3_2b))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_2a, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault3_2b, na=False, case=False))
    ),"tempsdg03_02"] = "SDG03_02"

print("Number of results = ", len(Data[(Data.tempsdg03_02 == "SDG03_02")])) 
```


```python
test=Data.loc[(Data.tempsdg03_02 == "SDG03_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.3

*By 2030, end the epidemics of AIDS, tuberculosis, malaria and neglected tropical diseases and combat hepatitis, water-borne diseases and other communicable diseases.*

*Innen 2030 stanse epidemiene av aids, tuberkulose, malaria og neglisjerte tropiske sykdommer, og bekjempe hepatitt, vannbårne sykdommer og andre smittsomme sykdommer*

#### Phrase 1


```python
#Termlists
termlist3_3a = ["communicable disease", "communicable illness",
                "overførbar sykdom", "overførbare sykdommer", "smittsom sykdom", "smittsomme sykdommer", "smittsam sjukdom", "smittsame sjukdommar"] 

termlist3_3b = ["prevent","combat","fight","tackl","reduc","alleviat","mitigat",
                "eradicat","eliminat","end","ended","ending",
                "treat","cure","vaccin","control",
                "epidemic","pandemic","outbreak","spread","transmission","occurrence","incidence","prevalence","risk","rate",
                "medicine","drug","intervention","therap",
                
                "hindr", "forebygg", "førebygg", "kjemp", "takl", "reduser", "reduksjon", "lett", "mink",
                "utrydd", "eliminer", "stopp", "stogg",
                "behandl", "kurer", "vaksine", "kontroll",
                "epidemi", "pandemi", "utbrudd", "utbrot", "spre", "smitte", "overføring", "forekom", "førekom", "tilfelle", "utbre", "risik",
                "medisin", "legemid", "intervensjon", "terap"
               ]

termlist3_3c = ["non-communicable disease", "non-communicable illness", "noncommunicable disease", "noncommunicable illness", 
                "ikke smittsom sykdom", "ikke-smittsom sykdom", "ikke-smittsomme sykdom", "ikkje-smittsam sjukdom", "ikkje smittsame sjukdom"]

termlist3_3d = ["infectious disease", "tropical illness",
                "non communicable and communicable","communicable and non communicable","non-communicable and communicable","communicable and non-communicable", "noncommunicable and communicable","communicable and noncommunicable",
                
                "overførbar", "tropisk sykdom", "tropiske sykdom", "tropesykdom", "tropisk sjukdom", "tropiske sjukdom", "tropesjukdom", 
                "ikke-smittsom og smittsom", "ikke-smittsomme og smittsomme", "smittsom og ikke-smittsom", "smittsomme og ikke-smittsomme","ikkje-smittsam og smittsam", "ikkje-smittsame og smittsame", "smittsam og ikkje-smittsam", "smittsame og ikkje-smittsame"]            

phrasedefault3_3a = r'(?:{})'.format('|'.join(termlist3_3a))
phrasedefault3_3b = r'(?:{})'.format('|'.join(termlist3_3b))
phrasedefault3_3c = r'(?:{})'.format('|'.join(termlist3_3c))
phrasedefault3_3d = r'(?:{})'.format('|'.join(termlist3_3d))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_3a, na=False, case=False))
        &(Data['result_title'].str.contains(phrasedefault3_3b, na=False, case=False))
    ) 
    & (~(Data['result_title'].str.contains(phrasedefault3_3c, na=False, case=False))&(~Data['result_title'].str.contains(phrasedefault3_3d, na=False, case=False)))
),"tempsdg03_03"] = "SDG03_03"

print("Number of results = ", len(Data[(Data.tempsdg03_03 == "SDG03_03")])) 
```


```python
test=Data.loc[(Data.tempsdg03_03 == "SDG03_03"), ("result_id", "result_title")]
test.iloc[0:10, ]
```

#### Phrase 2



```python
#Termlists 
termlist3_3e = ["water borne", "waterborne", "water-borne", "water-related", "diorrhea", "diarrhea", "contagious", "transmissible", "infectious",
                "vannbår", "vassbår", "vassbor", "vannrelatert", "diare", "smittsom", "smittsam", "smitte", "overførbar"]

termlist3_3f = ["disease", "infection", "epidemic", "illness", 
                "sykdom", "sjukdom", "infeksjon", "epidemi"]

termlist3_3g = ["hepatitis", "acquired immune deficiency syndrome", "acquired immuno-deficiency syndrome", "acquired immunodeficiency syndrome", "Human Immunodeficiency Virus", "prevent aids",
                "tuberculosis", "malaria", "cholera", "meningitis", "influenza", "avian influenza", "h5n1", "rubella", "diphteria", "japanese encephalitis", "measles", "mumps", "tetanus",
                "pertussis", "polio", "yellow fever", "sexually transmitted disease", "sexually transmitted infection", "syphilis", 
                "lower respiratory infection", "respiratory tract infection",
                "coronavirus", "covid", "sars-cov", "middle east respiratory syndrome", "severe acute respiratory syndrome",
                "crimean-congo haemorrhagic fever", "viral haemorrhagic fever", "ebola", "plague", "rift valley fever", "zika virus",
                "amebiasis", "cryptosporidiosis", "cryptosporidium infection", "giardiasis", "giardia infection", "shigellosis", "cronobacter infection",
                "acanthamoeba", "balamuthia", "naegleria", "sappinia", "typhoid", 
                "neglected tropical disease", "buruli ulcer", "chagas", "dengue", "chikungunya", "dracunculiasis", "guinea-worm disease", "echinococcosis", "foodborne trematodiases",
                "human african trypanosomiasis", "sleeping sickness", "leishmaniasis", "leprosy", "lymphatic filariasis", "mycetom", "chromoblastomycosis", "deep mycoses",
                "onchocerciasis", "river blindness", "rabies", "scabies", "schistosomiasis", "soil-transmitted helminthiasis", "hookworm", "roundworm", "whipworm", "ascaris lumbricoides",
                "trichuris trichiura", "necator americanus", "ancylostoma duodenale", "snakebite envenoming", "taeniasis", "cysticercosis", "trachoma", "yaws",
                "trichuris", "necator", "ancylostoma",
                
                "hepatitt", "ervervet immunsvikt syndrom-virus", "humant immunsviktvirus", "hindre aids",
                "tuberkulose", "kolera", "meningitt", "influensa", "røde hunder", "difteri", "japansk encefalitt", "meslinger", "kusma", "stivkrampe",
                "kikhoste", "gulfeber", "seksuelt overførbar", "syfilis", 
                "luftveisinfeksjon", 
                "koronavirus", 
                "krimfeber", "rift valley-feber", "zikavirus",
                "amøbiasis", "kryptosporidiose", "giardiainfeksjon", "shigellose", "enterobakterieinfeksjon", "tyfoidfeber",         
                "neglisjert tropesykdom", "neglisjerte tropesjukdom", "neglisjert tropesjukdom", "negliserte tropesjukdom", "burulisår", "ekinokkokose", "trematodeinfeksjon",
                "afrikansk trypanosomiasis", "lepra", "lymfatisk filariasis", "mykose", "kromomykose",
                "onkocerkose", "skabb", "helmintiasis", "jordoverført helminthiasis", "hakeorm", "rundorm", "guineaorm", 
                "taeniainfeksjon", "cysticerkose", "trakom", "frambøsi"
                ]
# "pest" (NO, = "plague" EN) is difficult to include as "pest" + "control" is noisy. 
termlist3_3i = ["HIV", "AIDS", "MERS", "SARS"]
termlist3_3j = ["prevent", "combat", "fight", "tackl", "reduc", "alleviat", "mitigat", "eradicat", "eliminat", "treat", "cure", "curing", "vaccinate", "control", "contain",
                "hindr", "forebygg", "førebygg", "nedkjemp", "takl", "overvinn", "lette", "utrydde", "elimin", "stopp", "stogg", "behandl", "kurer", "vaksiner", "kontroll"]

phrasedefault3_3e = r'(?:{})'.format('|'.join(termlist3_3e))
phrasedefault3_3f = r'(?:{})'.format('|'.join(termlist3_3f))
phrasedefault3_3g = r'(?:{})'.format('|'.join(termlist3_3g))
phrasedefault3_3i = r'(?:{})'.format('|'.join(termlist3_3i))
phrasedefault3_3j = r'(?:{})'.format('|'.join(termlist3_3j))

```


```python
#Search 
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault3_3e, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault3_3f, na=False, case=False))
        )
    |
        (
            (Data['result_title'].str.contains(phrasedefault3_3g, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault3_3i, na=False, case=True))
        )
    )
    & (Data['result_title'].str.contains(phrasedefault3_3j, na=False, case=False))
    ),"tempsdg03_03"] = "SDG03_03"

print("Number of results = ", len(Data[(Data.tempsdg03_03 == "SDG03_03")])) 
```


```python
test=Data.loc[(Data.tempsdg03_03 == "SDG03_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists 
termlist3_3k = ["hepatitis", "acquired immune deficiency syndrome", "acquired immuno-deficiency syndrome", "acquired immunodeficiency syndrome", "Human Immunodeficiency Virus", "prevent aids",
                "tuberculosis", "malaria", "cholera", "meningitis", "influenza", "avian influenza", "h5n1", "rubella", "diphteria", "japanese encephalitis", "measles", "mumps", "tetanus",
                "pertussis", "polio", "yellow fever", "sexually transmitted disease", "sexually transmitted infection", "syphilis", 
                "lower respiratory infection", "respiratory tract infection",
                "middle east respiratory syndrome", 
                "crimean-congo haemorrhagic fever", "viral haemorrhagic fever", "ebola", "plague", "rift valley fever", "zika virus",
                "amebiasis", "cryptosporidiosis", "cryptosporidium infection", "giardiasis", "giardia infection", "shigellosis", "cronobacter infection",
                "acanthamoeba", "balamuthia", "naegleria", "sappinia", "typhoid", 
                "neglected tropical disease", "buruli ulcer", "chagas", "dengue", "chikungunya", "dracunculiasis", "guinea-worm disease", "echinococcosis", "foodborne trematodiases",
                "human african trypanosomiasis", "sleeping sickness", "leishmaniasis", "leprosy", "lymphatic filariasis", "mycetom", "chromoblastomycosis", "deep mycoses",
                "onchocerciasis", "river blindness", "rabies", "scabies", "schistosomiasis", "soil-transmitted helminthiasis", "hookworm", "roundworm", "whipworm", "ascaris lumbricoides",
                "trichuris trichiura", "necator americanus", "ancylostoma duodenale", "snakebite envenoming", "taeniasis", "cysticercosis", "trachoma", "yaws",
                "trichuris", "necator", "ancylostoma",
                
                "hepatitt", "ervervet immunsvikt syndrom-virus", "humant immunsviktvirus", "hindre aids",
                "tuberkulose", "kolera", "meningitt", "influensa", "røde hunder", "difteri", "japansk encefalitt", "meslinger", "kusma", "stivkrampe",
                "kikhoste", "gulfeber", "seksuelt overførbar", "syfilis", 
                "luftveisinfeksjon", 
                "krimfeber", "rift valley-feber", "zikavirus",
                "amøbiasis", "kryptosporidiose", "giardiainfeksjon", "shigellose", "enterobakterieinfeksjon", "tyfoidfeber",         
                "neglisjert tropesykdom", "neglisjerte tropesjukdom", "neglisjert tropesjukdom", "negliserte tropesjukdom", "burulisår", "ekinokkokose", "trematodeinfeksjon",
                "afrikansk trypanosomiasis", "lepra", "lymfatisk filariasis", "mykose", "kromomykose",
                "onkocerkose", "skabb", "helmintiasis", "jordoverført helminthiasis", "hakeorm", "rundorm", "guineaorm", 
                "taeniainfeksjon", "cysticerkose", "trakom", "frambøsi"
                ]
termlist3_3k_caps = ["HIV", "AIDS", "MERS"]

termlist3_3l = ["epidemi", "pandemi", "outbreak", 
                "spread", "transmission", "occurrence", "incidence", "prevalence", "risk", "rate",
                "medicine", "vaccin", "cure", "treatment", "drug", "intervention", "therap",
                "antimalaria", "antiviral", "antibioti", "antiparasitic", "antihelminthic",

                "utbrudd", "utbrot", "spredning", "spreiing", "smitte", "overføring", "forekomst", "førekomst", "hendelse", "hending", "utbredelse", "utbreiing", "risik",
                "medisin", "vaksin", "behandl", "legemiddel", "medikament", "intervensjon", "terap", "antihelminti"
               ]

termlist3_3m = ["coronavirus", "covid", "sars-cov", "severe acute respiratory syndrome",
                "koronavirus"]
termlist3_3m_caps = ["SARS"]

termlist3_3n = ["epidemi", "pandemi", "outbreak",
                "utbrudd", "utbrot"]

termlist3_3o = ["pandemic response", "epidemic response", "outbreak response",
                "spread", "transmission", "occurrence", "incidence", "prevalence", "risk", " rate",
                "medicine", "vaccin", "cure", "treatment", "drug", "intervention", "therap",
                "antimalaria", "antiviral", "antibioti", "antiparasitic", "antihelminthic",

                "utbrudd", "utbrot", 
                "spredning", "spreiing", "smitte", "overføring", "forekomst", "førekomst", "hendelse", "hending", "utbredelse", "utbreiing", "risik",
                "medisin", "vaksin", "behandl", "legemiddel", "medikament", "intervensjon", "terap", "antihelminti"
               ]
# space before "rate" (EN) is intentional to avoid "generate"

phrasedefault3_3k = r'(?:{})'.format('|'.join(termlist3_3k))
phrasedefault3_3k_caps = r'(?:{})'.format('|'.join(termlist3_3k_caps))
phrasedefault3_3l = r'(?:{})'.format('|'.join(termlist3_3l))
phrasedefault3_3m = r'(?:{})'.format('|'.join(termlist3_3m))
phrasedefault3_3m_caps = r'(?:{})'.format('|'.join(termlist3_3m_caps))
phrasedefault3_3n = r'(?:{})'.format('|'.join(termlist3_3n))
phrasedefault3_3o = r'(?:{})'.format('|'.join(termlist3_3o))
```


```python
#Search 
#in this search, some termlists from the previous search (phrase 2), are reused: termlist3_3e, termlist3_3f, termlist3_3h, termlist3_3j
Data.loc[(
    (
        (
            ((Data['result_title'].str.contains(phrasedefault3_3e, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_3f, na=False, case=False)))
            |(Data['result_title'].str.contains(phrasedefault3_3k, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault3_3k_caps, na=False, case=True))
        )
    & (Data['result_title'].str.contains(phrasedefault3_3l, na=False, case=False)) 
    )
    |
    (
        (
            (Data['result_title'].str.contains(phrasedefault3_3m, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault3_3m_caps, na=False, case=True))
        )
        &
        (
            ((Data['result_title'].str.contains(phrasedefault3_3j, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_3n, na=False, case=False)))
            |(Data['result_title'].str.contains(phrasedefault3_3o, na=False, case=False))
        )
    )
),"tempsdg03_03"] = "SDG03_03"

print("Number of results = ", len(Data[(Data.tempsdg03_03 == "SDG03_03")])) 
```


```python
test=Data.loc[(Data.tempsdg03_03 == "SDG03_03"), ("result_id", "result_title")]
test.iloc[0:10, ]
```

### SDG 3.4

*By 2030, reduce by one third premature mortality from non-communicable diseases through prevention and treatment and promote mental health and well-being.*

*Innen 2030 redusere prematur dødelighet forårsaket av ikke-smittsomme sykdommer med en tredel gjennom forebygging og behandling, og fremme mental helse og livskvalitet*

#### Phrase 1


```python
#Termlists 
termlist3_4a = ["non communicable", "noncommunicable", "non-communicable", "non transmissible", "nontransmissible", "non-transmissible", 
                "non infectious", "noninfectious", "non-infectious", "auto immun", "autoimmun", "auto-immun",
                
                "ikke-smittsom", "ikkje-smittsam", "ikke smittsom", "ikkje smittsam"
               ]
termlist3_4b = ["disease", "illness", 
                "sykdom", "sjukdom"
               ]
termlist3_4c = ["cardiovascular disease", "heart disease", "heart attack", "stroke", "diabetes",
                "chronic respiratory disease", "asthma", "emphysema", "chronic obstructive pulmonary disease",
                "COPD", "chronic obstructive airway disease", "chronic bronchitis", 
                "cancer", "sarcoma", "carcinoma", "blastoma", "myeloma", "lymphoma", "leukaemia", "leukemia",
                "mesothelioma", "melanom", "kidney disease", "alzheimer", "dementia", "cirrhosis",
                
                "kardiovaskulær sykdom", "kardiovaskulære sykdom", "kardiovaskulær sjukdom", "kardiovaskulære sjukdom",
                "hjertesykdom", "hjartesjukdom", "hjerteinfarkt", "hjarteinfarkt", "hjerteanfall", "hjarteanfall", "hjerteattakk", "hjarteattakk", "slag",
                "kronisk luftvei", "astma", "emfysem", "kronisk obstruktiv lungesykdom", "kronisk obstruktiv lungesjukdom", "kols", "kronisk bronkitt",
                "kreft", "sarkom", "karsinom", "blastom", "lymfom", "leukemi",
                "mesoteliom", "nyresykdom", "nyresjukdom", "demens"
               ]
termlist3_4d = ["chronic", 
                "kronisk"]
termlist3_4e = ["lung", 
                "pulmonar"]    
termlist3_4f = ["malignant", "incurable", "malign", 
                "ondart", "vondarta", "uhelbredelig"] 
termlist3_4g = ["neoplasm", "tumour", 
                "tumor", "svulst"]  
termlist3_4h = ["mortalit", "death", "surviv", 
                "dødelighet", "overlev"]                         

phrasedefault3_4a = r'(?:{})'.format('|'.join(termlist3_4a))
phrasedefault3_4b = r'(?:{})'.format('|'.join(termlist3_4b))
phrasedefault3_4c = r'(?:{})'.format('|'.join(termlist3_4c))
phrasedefault3_4d = r'(?:{})'.format('|'.join(termlist3_4d))
phrasedefault3_4e = r'(?:{})'.format('|'.join(termlist3_4e))
phrasedefault3_4f = r'(?:{})'.format('|'.join(termlist3_4f))
phrasedefault3_4g = r'(?:{})'.format('|'.join(termlist3_4g))
phrasedefault3_4h = r'(?:{})'.format('|'.join(termlist3_4h))
```


```python
#Search 
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault3_4a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_4b, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault3_4c, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault3_4d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_4e, na=False, case=False))) 
        |((Data['result_title'].str.contains(phrasedefault3_4f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_4g, na=False, case=False)))
    )
    & (Data['result_title'].str.contains(phrasedefault3_4h, na=False, case=False))
),"tempsdg03_04"] = "SDG03_04"

print("Number of results = ", len(Data[(Data.tempsdg03_04 == "SDG03_04")]))

```


```python
test=Data.loc[(Data.tempsdg03_04 == "SDG03_04"), ("result_id", "result_title")]
test.iloc[0:10, ]
```

#### Phrase 2


```python
#Termlists
termlist3_4h = ["mental health disorder", "mental illness", "suicid", "depression", "depressive disorder",
                "bipolar affective disorder", "schizophrenia", "psychosis", "psychoses",
                
                "psykisk lidelse", "psykisk liding", "psykisk syk", "psykisk sjuk", "selvmord", "sjølmord", "sjølvmord", "depresjon", "depressiv lid",
                "bipolar lid", "schizofreni", "psykose"
               ]
termlist3_4i = ["prevent", "combat", "fight", "reduc", "alleviat", "eradicat", "eliminat", "tackl", "treat", "cure",
                "epidemi", "occurrence", "incidence", "prevalence", "risk", "rate",
                "medicine", "vaccin", "drug", "treatment", "intervention", "therap",
                "outreach", "services", "support", "counseling", "counselling",
                
                "hindr", "forebygg", "førebygg", "kjemp", "reduser", "reduksjon", "utrydd", "eliminer", "takl", "behandl", "kurer", 
                "forekom", "førekom", "hendelse", "hending", "tilfelle", "utbre", "risik",
                "medisin", "vaksin", "legemid", "medikament", "behandling", "intervensjon", "terap",
                "støtte", "stønad", "tjeneste", "teneste", "rådgiv", "rådgjev"
               ]       
                            
phrasedefault3_4h = r'(?:{})'.format('|'.join(termlist3_4h))
phrasedefault3_4i = r'(?:{})'.format('|'.join(termlist3_4i))
```


```python
#Search 3_4hi
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_4h, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault3_4i, na=False, case= False)) 
    ),"tempsdg03_04"] = "SDG03_04"

print("Number of results = ", len(Data[(Data.tempsdg03_04 == "SDG03_04")])) 
```

#### Phrase 3


```python
#Termlists
termlist3_4j = ["mental health", "well being", "wellbeing", "well-being",
                "mental helse", "velvære", "god helse"
               ]
termlist3_4k = ["promot", "strengthen", "improv", "enhanc", "medicine", "vaccin", "drug", "cure", "treatment", "intervention", 
                "therap", "outreach", "services", "support", "counselling", "counseling",

                "fremme", "fremje", "styrke", "bedre", "betre", "øke", "auke", "medisin", "vaksine", "medikament", "legemid", "kurer", "behandl", "intervensjon"
                "terap", "tjeneste", "teneste", "støtte", "stønad", "rådgi", "rådgje"
               ]
termlist3_4l = ["reduc", "decreas", 
                "reduser", "mink"
               ]
termlist3_4m = ["problem"]     


phrasedefault3_4j = r'(?:{})'.format('|'.join(termlist3_4j))
phrasedefault3_4k = r'(?:{})'.format('|'.join(termlist3_4k))
phrasedefault3_4l = r'(?:{})'.format('|'.join(termlist3_4l))
phrasedefault3_4m = r'(?:{})'.format('|'.join(termlist3_4m))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_4j, na=False, case=False)) 
    &
    (
        (Data['result_title'].str.contains(phrasedefault3_4k, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasedefault3_4l, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault3_4m, na=False, case=False))
        )
    )  
),"tempsdg03_04"] = "SDG03_04"

print("Number of results = ", len(Data[(Data.tempsdg03_04 == "SDG03_04")])) 
```


```python
test=Data.loc[(Data.tempsdg03_04 == "SDG03_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.5

*Strengthen the prevention and treatment of substance abuse, including narcotic drug abuse and harmful use of alcohol.*

*Styrke forebygging og behandling av rusmiddelmisbruk, blant annet misbruk av narkotiske stoffer og skadelig bruk av alkohol*



```python
#Termlists
termlist3_5a = ["binge drinking", "binge drinker", "alcohol", "excessive drinking", "problematic drinking", "problem drinking",
                "substance use", "illicit drugs", "people who inject drugs", "PWID", "opiod epidemic",
                
                "alkohol", "periodedrank", "periodedrikk", "narkotikamisbruk", "stoffmisbruk", "opioidepidemi"
               ]
termlist3_5atrunk = ["fyll"]  

termlist3_5b = ["drug", "narcotic", "substance", "alcohol", "amphetamine", "metamphetamine", "MDMA", "ecstacy", "cocaine", "inhalant", "amyl nitrate",
                "marijuana", "cannabis", "opioid", "opiat", "heroin", "morphine", "phencyclidine", "LSD", "psilocybin", "dimethyltriptamin", "khat", "tobacco",
                
                "rusmid", "narkotik", "stoff", "alkohol", "amfetamin", "metamfetamin", "kokain", "inhalasjon", "inhalering", "amylnitrat", 
                "marihuana", "hasj", "morfin", "fensyklidin", "tobakk"
               ]

termlist3_5c = ["abuse", "misuse", "dependence", "addict", 
                "overdose", "misbruk", "avheng"]

termlist3_5d = ["use", "usage", "consumption",
                "bruk", "forbruk"]

termlist3_5e = ["harmful", "problematic", "excessive", "disorder",
                "skadelig", "skadeleg", "problematisk", "overdreven", "overdriven", "lidelse", "liding"]  

termlist3_5f = ["prevent", "combat", "tackl", "fight against", "reduc", "decrease", "minimi", "limit", "alleviat", "mitigat", "eradicat", "eliminat", "stop", "treat", "control",
                "hindr", "forebygg", "førebygg", "takl", "kjemp", "reduser", "reduksjon", "grens", "utrydd", "eliminer", "kontroll"]

termlist3_5g = ["medicine", "cure", "treatment", "intervention", "therapy", "therapies", "outreach", "services", "support", "rehabilitat", "aftercare", "counseling", "counselling",
                "medisin", "kurer", "behandl", "intervensjon", "terapi", "tjeneste", "teneste", "støtte", "stønad", "rehabiliter", "rådgi", "rådgje"]                
                
phrasedefault3_5a = r'(?:{})'.format('|'.join(termlist3_5a))
phrasespecific3_5atrunk = r'\b(?:{})\b'.format('|'.join(termlist3_5atrunk))
phrasedefault3_5b = r'(?:{})'.format('|'.join(termlist3_5b))
phrasedefault3_5c = r'(?:{})'.format('|'.join(termlist3_5c))
phrasedefault3_5d = r'(?:{})'.format('|'.join(termlist3_5d))
phrasedefault3_5e = r'(?:{})'.format('|'.join(termlist3_5e))
phrasedefault3_5f = r'(?:{})'.format('|'.join(termlist3_5f))
phrasedefault3_5g = r'(?:{})'.format('|'.join(termlist3_5g))
```


```python
#Search 3_5abcdefg
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_5a, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific3_5atrunk, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasedefault3_5b, na=False, case=False)) 
            &
            (
                (Data['result_title'].str.contains(phrasedefault3_5c, na=False, case=False))
                |((Data['result_title'].str.contains(phrasedefault3_5d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_5e, na=False, case=False)))
            )   
        )
    )
    &
    (
        (Data['result_title'].str.contains(phrasedefault3_5f, na=False, case=False))
        |(Data['result_title'].str.contains(phrasedefault3_5g, na=False, case=False))
    )
),"tempsdg03_05"] = "SDG03_05"

print("Number of results = ", len(Data[(Data.tempsdg03_05 == "SDG03_05")]))
```


```python
test=Data.loc[(Data.tempsdg03_05 == "SDG03_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.6

*By 2020, halve the number of global deaths and injuries from road traffic accidents.*

*Innen 2030 halvere antall dødsfall og skader i verden forårsaket av trafikkulykker*


In the Web of science search, "air traffic" and "boat traffic" were excluded using NOT, but that does not seem necessary in this search. A few hits with metaphorical use of terms like "road" and "death" are hard to avoid.



```python
#Termlists
termlist3_6a = ["traffic", "roadway", "street", "roundabout", "highway", "motorway", "cycling lane", "cycle path", "bicycle lane",
                "walkway", "walking path", "sidewalk", "pavement", "bicycles", "motorcycles", "motorbike", "automobile", "lorry", "lorries", "truck", "pedestrian", "cyclist", 
                "driving fatalit",

                "trafikk", "rundkjøring", "rundkøyring", "motorvei", "motorveg", "sykkelsti", "sykkelve",
                "gangve", "fortau", "sykkel", "sykler", "syklar", "motorsykkel", "motorsykler", "motorsyklar", "buss", "fotgjenger", "syklist", "syklende", "syklande", 
                "trafikkdød", "trafikkulykke", "trafikkulukke", "bilulykke", "bilulukke"]

termlist3_6atrunk = ["bus", "buses", "HGV", "HGVs", "SUV", "SUVs", "road", "roads",
                     "vei", "veier", "veg", "veger", "vegar", "gående", "gåande"]

termlist3_6btrunk = ["vehicle.*", "driver.*", "driving", "car", "cars",
                     "kjøretøy.*", "køyretøy.*", ".*fører", ".*førar", ".*sjåfør.*", "kjøring", "køyring", "bil", "biler", "bilar"]

termlist3_6c = ["accident", "crash", "collision", "incident",
                "ulykke", "ulukke", "kræsj", "kollisjon", "traffikhend"]

termlist3_6c_case = ["RTI", "RTIs"]

termlist3_6d = ["mortal", "death", "fatal", "deadly", "morbidity", "injury", "injuries", "injured", "road trauma",
                "dødelig", "dødeleg", "døyeleg", "død", "skade", "skadd"]

termlist3_6e = ["driver", "road", "cycling", "cyclist", "bicycle", "pedestrian", "vehicle"
                
                "fører", "førar", "sjåfør", "vei", "veier", "veg", "veger", "vegar", "sykler", "syklar", "syklist", "syklende", "syklande", "sykkel",
                "fotgjenger", "fotgjengar", "gående", "gåande", "kjøretøy", "køyretøy"]

#termlist3_6f = ["air traffic", "boat traffic"]

phrasedefault3_6a = r'(?:{})'.format('|'.join(termlist3_6a))
phrasespecific3_6atrunk = r'\b(?:{})\b'.format('|'.join(termlist3_6atrunk))
phrasespecific3_6btrunk = r'\b(?:{})\b'.format('|'.join(termlist3_6btrunk))
phrasedefault3_6c = r'(?:{})'.format('|'.join(termlist3_6c))
phrasespecific3_6c_case = r'\b(?:{})\b'.format('|'.join(termlist3_6c_case))
phrasedefault3_6d = r'(?:{})'.format('|'.join(termlist3_6d))
phrasedefault3_6e = r'(?:{})'.format('|'.join(termlist3_6e))
#phrasedefault3_6f = r'(?:{})'.format('|'.join(termlist3_6f))
```


```python
#Search 3_6Prenatal and childhood exposure to air pollution and traffic and the risk of liver injury in European children 	
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_6a, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific3_6atrunk, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasespecific3_6btrunk, na=False, case=False)) 
            & ((Data['result_title'].str.contains(phrasedefault3_6c, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific3_6c_case, na=False, case=True)))
        )
    )
    & ((Data['result_title'].str.contains(phrasedefault3_6d, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific3_6c_case, na=False, case=True)))
    & 
    (
        ((Data['result_title'].str.contains(phrasedefault3_6c, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific3_6c_case, na=False, case=True)))
        |((Data['result_title'].str.contains(phrasedefault3_6d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_6e, na=False, case=False)))
    )
),"tempsdg03_06"] = "SDG03_06"

print("Number of results = ", len(Data[(Data.tempsdg03_06 == "SDG03_06")]))
```


```python
test=Data.loc[(Data.tempsdg03_06 == "SDG03_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.7

*By 2030, ensure universal access to sexual and reproductive health-care services, including for family planning, information and education, and the integration of reproductive health into national strategies and programmes*

*Innen 2030 sikre allmenn tilgang til tjenester knyttet til seksuell og reproduktiv helse, inkludert familieplanlegging og tilhørende informasjon og opplæring, og sikre at reproduktiv helse innarbeides i nasjonale strategier og programmer*

#### Phrase 1


```python
#Termlists
termlist3_7a = ["reproductive health", "sexual health", "family planning", "planned pregnanc", "contracept", "abortion",
                "reproduksjonshelse", "reproduktiv helse", "seksuell helse", "familieplanlegging", "planlagt graviditet", "prevensjon", "abort"]

termlist3_7b = ["reproduct", "sex", 
                "reproduk"]

termlist3_7c = ["education", "inform", "health literacy", 
                "utdann", "opplær", "opplys", "kompetanse"]

termlist3_7d = ["health equity", "equality in health", "health for all", "health promotion",
                "access", "right", "coverage", "afford", "low cost", "free of charge", "free service", "subsidi",
                "barrier", "obstacle", "impediment", "unaffordab", "expensive",
                
                "rettferdig helse", "helsefrem",
                "tilgang", "adgang", "åtgang", "rett", "dekning", "rimelig", "rimeleg", "billig", "billeg", "gratis", "hindr", "hinder", "dyr", "kostbar"
               ]

phrasedefault3_7a = r'(?:{})'.format('|'.join(termlist3_7a))
phrasedefault3_7b = r'(?:{})'.format('|'.join(termlist3_7b))
phrasedefault3_7c = r'(?:{})'.format('|'.join(termlist3_7c))
phrasedefault3_7d = r'(?:{})'.format('|'.join(termlist3_7d))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_7a, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault3_7b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_7c, na=False, case=False)))  
    )
    & (Data['result_title'].str.contains(phrasedefault3_7d, na=False, case=False)) 
),"tempsdg03_07"] = "SDG03_07"

print("Number of results = ", len(Data[(Data.tempsdg03_07 == "SDG03_07")]))
```


```python
#Results
test=Data.loc[(Data.tempsdg03_07 == "SDG03_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists  
termlist3_7e = ["reproductive health", "sexual health", "family planning", "planned pregnanc", "contracept", "abortion",
                "reproduksjonshelse", "reproduktiv helse", "seksuell helse", "familieplanlegging", "planlagt graviditet", "prevensjon", "abort"]

termlist3_7f = ["reproduct", "sex", 
                "reproduk"]

termlist3_7g = ["education", "inform", "health literacy", 
                "utdann", "opplær", "opplys", "kompetanse"]

termlist3_7h = ["policy", "policies", "initiativ", "framework", "program", "plan ",
                "strateg", "politikk", "retningslin", "rammeverk", "planlegg"]

termlist3_7i = ["national", "state", "federal", 
                "nasjonal", "stat"]

phrasedefault3_7e = r'(?:{})'.format('|'.join(termlist3_7e))
phrasedefault3_7f = r'(?:{})'.format('|'.join(termlist3_7f))
phrasedefault3_7g = r'(?:{})'.format('|'.join(termlist3_7g))
phrasedefault3_7h = r'(?:{})'.format('|'.join(termlist3_7h))
phrasedefault3_7i = r'(?:{})'.format('|'.join(termlist3_7i))
```


```python
#Search 1
Data.loc[(
    (
       (Data['result_title'].str.contains(phrasedefault3_7e, na=False, case=False))
       |((Data['result_title'].str.contains(phrasedefault3_7f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_7g, na=False, case=False)))
    )
    & (Data['result_title'].str.contains(phrasedefault3_7h, na=False, case=False))
    & 
    (
        (Data['LMICs']==True)
        |(Data['result_title'].str.contains(phrasedefault3_7i, na=False, case=False))
    )
),"tempsdg03_07"] = "SDG03_07"

print("Number of results = ", len(Data[(Data.tempsdg03_07 == "SDG03_07")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg03_07 == "SDG03_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.8

*Achieve universal health coverage, including financial risk protection, access to quality essential health-care services and access to safe, effective, quality and affordable essential medicines and vaccines for all*

*Oppnå allmenn dekning av helsetjenester, inkludert ordninger som beskytter mot økonomiske konsekvenser, og allmenn tilgang til grunnleggende og gode helsetjenester og trygge, virksomme og nødvendige medisiner og vaksiner av god kvalitet og til en overkommelig pris*

#### Phrase 1


```python
#Termlists
termlist3_8a = ["universal health coverage", "universal healthcare", "universal health care",
                
                "universell helsedekning", "allmenn dekning av helsetenester", "allmenn dekning av helsetjenester", "allmenn tilgang til helsetjenester",
                "allmenn tilgang til helsetenester", "allment tilgjengelige helsetjenester", "allment tilgjengelege helsetenester",
                "helsetjenester for alle", "helsetenester for alle"]

phrasedefault3_8a = r'(?:{})'.format('|'.join(termlist3_8a))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_8a, na=False, case=False)) 
    ),"tempsdg03_08"] = "SDG03_08"

print("Number of results = ", len(Data[(Data.tempsdg03_08 == "SDG03_08")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg03_08 == "SDG03_08"), ("result_id", "result_title")]
test.iloc[0:10, ]
```

#### Phrase 2



```python
#Termlists
termlist3_8b = ["health care", "healthcare", "health service", "medical service", "medical care", "health coverage", "family planning", "reproductive health", "sexual health",
                "vaccin", "immunisation", "immunization", "treatment access", "access to treatment",
                
                "helsehjelp", "helsetjeneste", "helseteneste", "omsorgstjeneste", "omsorgsteneste", "helsedekning", "familieplanlegging", "reproduksjonshelse", "reproduktiv helse", 
                "seksuell helse", "vaksin", "immunisering", "tilgang til behandling"]

termlist3_8c = ["essential", "basic", "life saving", "necessary", "emergency",
                "essensiell", "nødvendig", "grunnlegg", "livred", "nødvendig", "naudsynt", "nødstilfelle", "naudstilfelle"]

termlist3_8d = ["medicines", "medication", "treatment", "therap",
                "medisin", "behandl", "terap"]

termlist3_8e = ["health equity", "equity in health", "health care equity", "equity in healthcare", "health for all", "vaccine equity", 
                "access", "barrier", "obstacle", 
                "afford", "low cost", "inexpensive", "free service", "free of charge", "voucher", "high price", "costly", "debt", "financial risk", "financial burden",
                "financial hardship", "household expenditure", "medical expenditure", "medical expenses", "medical bill", "medical cost", "out of pocket", "microinsurance",
                "quality medicines", "quality care", "quality of care", "quality health care",

                "rettferdig helse", "rettferdig vaksine", 
                "tilgang", "adgang", "åtgang", "hindr", "hinder", "rimelig", "rimeleg", "billig", "billeg", "gratis", "høy pris", "høg pris",
                "kostbar", "økonomisk risiko", "økonomisk byrde", "økonomisk besvær", "økonomisk vansk", "økonomiske vansk", "husholdningsutgift", "hushaldningsutgift", 
                "medisinsk utgift", "medisinske utgift", "helseutgift", "legeregning", "legerekning", "sykehusregning", "sjukehusrekning", "behandlingsutgift", "mikroforsikring"]                    
    
phrasedefault3_8b = r'(?:{})'.format('|'.join(termlist3_8b))
phrasedefault3_8c = r'(?:{})'.format('|'.join(termlist3_8c))
phrasedefault3_8d = r'(?:{})'.format('|'.join(termlist3_8d))
phrasedefault3_8e = r'(?:{})'.format('|'.join(termlist3_8e))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_8b, na=False, case=False)) 
        |((Data['result_title'].str.contains(phrasedefault3_8c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_8d, na=False, case=False))) 
    )
    & (Data['result_title'].str.contains(phrasedefault3_8e, na=False, case=False))  
),"tempsdg03_08"] = "SDG03_08"

print("Number of results = ", len(Data[(Data.tempsdg03_08 == "SDG03_08")])) 
```


```python
test=Data.loc[(Data.tempsdg03_08 == "SDG03_08"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.9

*By 2030, substantially reduce the number of deaths and illnesses from hazardous chemicals and air, water and soil pollution and contamination*

*Innen 2030 betydelig redusere antall dødsfall og sykdomstilfeller forårsaket av farlige kjemikalier og forurenset luft, vann og jord*


#### Phrase 1


```python
#Termlists
termlist3_9a = ["air pollution", "particular matter", "ozon", 
                "luftforurensing", "luftforurensning", "luftforureining", "partik"]

termlist3_9b = ["PM2.5", "PM10"]

termlist3_9c = ["nitrogen dioxide", "sulfur dioxide", "sulphur dioxide", "carbon monoxide", "volatile organic compounds",
                "nitrogendioksid", "svoveldioksid", "karbonmonoksid", "flyktig organisk forbindelse", "flyktige organiske forbindelse"]

termlist3_9d = ["pollution", "poisoning", 
                "forurensing", "forurensning", "forureining", "forgift"]

termlist3_9e = ["smoke pollution", "secondhand smok", "second hand smok", "involuntarily smoking", "passive smoking", 
                "røykforurensning", "røykforurensing", "røykforureining", "passiv røyk"]

termlist3_9f = ["drinking water", "potable water", "water source", 
                "drikkevann", "drikkevatn", "drikkevass", "vannkilde", "vasskjelde"]

termlist3_9g = ["unsafe", "safe", "contaminated", "contamination", "pollut", "clean", 
                "tryg", "forurens", "forurein", "ren", "rein"]

termlist3_9h = ["poor hygiene", "good hygiene", "hand hygiene", "personal hygiene", "hygiene practice", "hygiene intervention", "handwashing", "poor sanitation",
                "adequate sanitation", "good sanitation", "sanitation facilities", "water sanitation and hygiene",
                
                "dårlig hygien", "god hygien", "håndhygien", "handhygien", "personlig hygien", "personleg hygien", "hygien", "håndvask", "handvask", "sanitær"]

termlist3_9i = ["food",
                "mat", "føde"]

termlist3_9j = ["unsafe", "contaminated", "contamination", "sanitation", 
                "utryg", "forurens", "forurein", "sanitet", "sanitær"]

termlist3_9k = ["food poisoning", "foodborne pathogens", 
                "matforgift", "matbår"]

termlist3_9l = ["poisoning", 
                "forgift"]

termlist3_9m = ["unintentional", "accidental", 
                "ikke-intendert", "uintendert", "tilfeldig"]    

termlist3_9n = ["mortality", "death", "illness", "disease", "morbidity", "poisoning", 
                "død", "dau", "sykdom", "sjukdom", "forgift"]             

phrasedefault3_9a = r'(?:{})'.format('|'.join(termlist3_9a))
phrasedefault3_9b = r'(?:{})'.format('|'.join(termlist3_9b))
phrasedefault3_9c = r'(?:{})'.format('|'.join(termlist3_9c))
phrasedefault3_9d = r'(?:{})'.format('|'.join(termlist3_9d))
phrasedefault3_9e = r'(?:{})'.format('|'.join(termlist3_9e))
phrasedefault3_9f = r'(?:{})'.format('|'.join(termlist3_9f))
phrasedefault3_9g = r'(?:{})'.format('|'.join(termlist3_9g))
phrasedefault3_9h = r'(?:{})'.format('|'.join(termlist3_9h))
phrasedefault3_9i = r'(?:{})'.format('|'.join(termlist3_9i))
phrasedefault3_9j = r'(?:{})'.format('|'.join(termlist3_9j))
phrasedefault3_9k = r'(?:{})'.format('|'.join(termlist3_9k))
phrasedefault3_9l = r'(?:{})'.format('|'.join(termlist3_9l))
phrasedefault3_9m = r'(?:{})'.format('|'.join(termlist3_9m))
phrasedefault3_9n = r'(?:{})'.format('|'.join(termlist3_9n))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_9a, na=False, case=False))
        |(Data['result_title'].str.contains(phrasedefault3_9b, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault3_9c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_9d, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault3_9e, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault3_9f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_9g, na=False, case=False)) )
        |(Data['result_title'].str.contains(phrasedefault3_9h, na=False, case=False))       
        |((Data['result_title'].str.contains(phrasedefault3_9i, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_9j, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault3_9k, na=False, case=False)) 
        |((Data['result_title'].str.contains(phrasedefault3_9l, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_9m, na=False, case=False)))
    )          
    & (Data['result_title'].str.contains(phrasedefault3_9n, na=False, case=False))      
),"tempsdg03_09"] = "SDG03_09"

print("Number of results = ", len(Data[(Data.tempsdg03_09 == "SDG03_09")])) 
```


```python
test=Data.loc[(Data.tempsdg03_09 == "SDG03_09"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2

In this search it proved hard to exclude noise eg. from articles concerning animals. We could not use "human" terms to delimit the search as we did in Web of Science, as this excluded too many relevant hits. Sometimes articles which have animal names in the title, are ultimately concerned with issues relating to human conditions, therefore they shoud be included. It is also hard to specify species to include/exclude, as we cannot know or predict which may be used in what context.


```python
#Termlists
termlist3_9o = ["hazardous chemical", "hazardous material", "hazardous substance", "hazardous waste", "pollution", 
                "soil contamination", "contamination of soils", "water contamination","contamination of water", 
                "arsenic", "asbestos", "benzen", "cadmium", "dioxin", "mercury", "fluoride", "pesticide", 
                "lead poison", "lead toxicity", "lead-mediated toxicity", "lead-induced toxicity", "lead exposure", "lead carcinogen", "blood lead", 
                "radioactive waste", "persistent organic pollutant", "sanitation",

                "farlige kjemikalier", "farlege kjemikaliar", "farlige materialer", "farlege materialar", "farlige stoff", "farlege stoff", "farlig avfall", "farleg avfall", 
                "forurensing", "forurensning", "forureining", "forurenset grunn", "forureina grunn", 
                "arsenikk", "asbest", "kadmium", "dioksin", "kvikksølv", "fluor", "pesticid", "plantevernmiddel",
                "blyforgift", "blyeksponering", 
                "radioaktivt avfall", "miljøgift"
               ]

termlist3_9p = ["mortality", "death", "illness", "disease", "morbidity", "toxicity", "poisoning", "poisoned", "fluorosis",
                "dødelighet", "dødelegheit", "død", "daud", "sykdom", "sjukdom", "toksisitet", "forgift", "fluorose"
               ]
#termlist3_9q = ["human", "humanity", "people", "person", "child", "under fives", "infant", "toddler", "babies", "teenager", "adolescent", "girls", "boys", "elderly", "adult", "women", 
#                "woman", "rural", "urban", "cities", "town", "village", "countr", "nation", "developed state", "developing state",
#                "patient", "hospital", "premature death", "premature mortality", "neglected tropical disease", "diarrhoea", "diarrhea",
#                "menneske", "folk", "person", "barn", "unge", "spedbarn", "baby", "nyfød", "tenåring", "ungdom", "jente", "eldre", "voksen", "vaksen", "voksne", "vaksne", "kvinne",
#                "land", "nasjon", "pasient", "sykehus", "sjukehus", "prematur", "neglisjerte tropesykdommer", "neglisjerte tropesjukdom", "diare"]
#Not used - see comment over.

phrasedefault3_9o = r'(?:{})'.format('|'.join(termlist3_9o))
phrasedefault3_9p = r'(?:{})'.format('|'.join(termlist3_9p))
#phrasedefault3_9q = r'(?:{})'.format('|'.join(termlist3_9q))
```


```python
Data.loc[( 
    (Data['result_title'].str.contains(phrasedefault3_9o, na=False, case=False))
    &(Data['result_title'].str.contains(phrasedefault3_9p, na=False, case=False))   
),"tempsdg03_09"] = "SDG03_09"

print("Number of results = ", len(Data[(Data.tempsdg03_09 == "SDG03_09")])) 
```


```python
test=Data.loc[(Data.tempsdg03_09 == "SDG03_09"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.a

*Strengthen the implementation of the World Health Organization Framework Convention on Tobacco Control in all countries, as appropriate*

*Styrke gjennomføringen av Verdens helseorganisasjons rammekonvensjon om forebygging av tobakksskader i alle land*

#### Phrase 1


```python
#Termlists
termlist3_a1 = ["framework convention on tobacco control", 
                "tobakkskonvensjon", "konvensjon om forebygging av tobakksskad"]
termlist3_a2 = ["FCTC"]                
              
phrasedefault3_a1 = r'(?:{})'.format('|'.join(termlist3_a1))
phrasedefault3_a2 = r'(?:{})'.format('|'.join(termlist3_a2))
```


```python
#search
Data.loc[(
         (Data['result_title'].str.contains(phrasedefault3_a1, na=False, case=False))
         |(Data['result_title'].str.contains(phrasedefault3_a2, na=False, case=True))   
    ),"tempsdg03_a"] = "SDG03_0a"

print("Number of results = ", len(Data[(Data.tempsdg03_a == "SDG03_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg03_a == "SDG03_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2

When searching only titles, the approach used in the Web of Science search proved too restrictive. Many articles talk about smoke cessation etc. without mentioning "tobacco", therefore we have built the search without "tobacco" as a necessary term, even though this leads to some noise. 


```python
#Termlists
termlist3_a3 = ["tobacco", "smoking", "cigarette", 
                "tobakk", "røyking", "sigarett"]

termlist3_a4 = ["reduc", "control", "ban", "prohibit", "legislation", "policy", "policies", "regulat", "law", "strateg", "intervention", "tax", "health warning",
                "smoking cessation", "quitting", "services", "cessation service", "cessation program", "alternativ",
                
                "reduser", "reduksjon", "kontroll", "forby", "forbud", "forbod", "lovgivning", "lovgiving", "politikk", "retningslin", "reguler", "lov", "strategi", "intervensjon", "inngrip",
                "skatt", "helseadvarsel", "helseåtvaring", "røykeslutt", "røykestopp", "slutt", "stopp", "tjeneste", "teneste"]

termlist3_a5 = ["reduce tobacco", "reduce smoking", "decrease tobacco", "reduce dependence on tobacco", 
                "redusere avhengig"]    

#termlist3_a6 = ["tobacco", "tobakk"]            
#Not used, see comment over

phrasedefault3_a3 = r'(?:{})'.format('|'.join(termlist3_a3))
phrasedefault3_a4 = r'(?:{})'.format('|'.join(termlist3_a4))
phrasedefault3_a5 = r'(?:{})'.format('|'.join(termlist3_a5))
#phrasedefault3_a6 = r'(?:{})'.format('|'.join(termlist3_a6))
```


```python
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_a3, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault3_a4, na=False, case=False))
    )
    |(Data['result_title'].str.contains(phrasedefault3_a5, na=False, case=False))             
),"tempsdg03_a"] = "SDG03_0a"

print("Number of results = ", len(Data[(Data.tempsdg03_a == "SDG03_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg03_a == "SDG03_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3



```python
#Termlists 
termlist3_a7 = ["tobacco farm", "tobacco production", "tobacco growing", "tobacco grower", 
                "tobakksproduksjon", "produksjon av tobakk", "tobakksdyrk", "dyrking av tobakk", "tobakksbonde", "tobakksbønder"]

termlist3_a8 = ["alternativ", "diversif", "alternative crop", "crop substitution", "alternative livelihood", "sustainable livelihood",
                "divers", "alternativt jordbruk", "alternativ avling", "alternativt levebrød", "alternative inntektsk", "bærekraftig levebrød", "berekraftig levebrød"]

phrasedefault3_a7 = r'(?:{})'.format('|'.join(termlist3_a7))
phrasedefault3_a8 = r'(?:{})'.format('|'.join(termlist3_a8))
```


```python
#search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_a7, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault3_a8, na=False, case=False))
    ),"tempsdg03_a"] = "SDG03_0a"

print("Number of results = ", len(Data[(Data.tempsdg03_a == "SDG03_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg03_a == "SDG03_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.b

*Support the research and development of vaccines and medicines for the communicable and non‑communicable diseases that primarily affect developing countries, provide access to affordable essential medicines and vaccines, in accordance with the Doha Declaration on the TRIPS Agreement and Public Health, which affirms the right of developing countries to use to the full the provisions in the Agreement on Trade-Related Aspects of Intellectual Property Rights regarding flexibilities to protect public health, and, in particular, provide access to medicines for all*

*Støtte forskning på – og utvikling av – vaksiner og medisiner mot smittsomme og ikke-smittsomme sykdommer som primært rammer utviklingsland, sørge for tilgang til nødvendige medisiner og vaksiner til en overkommelig pris, i samsvar med Doha-erklæringen om TRIPS-avtalen og folkehelse, som bekrefter utviklingslandenes rett til fullt ut å anvende bestemmelsene som gjelder adgangen til å verne om folkehelsen og særlig sørge for tilgang til medisiner for alle, i avtalen om handelsrelaterte aspekter ved immaterielle rettigheter*

#### Phrase 1


```python
#Termlists
#termlist3_b1 = ["develop", "research", "r&d", "r & d",
#                "utvikl", "forskning", "FOU"]

termlist3_b2 = ["new medicine", "novel medicin", "new medicatio", "novel medication", "new therap", "novel therap",
                "new vaccin", "novel vaccin", "vaccine development",
                "new drug", "novel drug", "drug development", "drug discovery", "new cure", "novel cure", "new treatment", "novel treatment",

                "ny medisin", "nye medisin", "nytt medikament", "nye medikament", "ny terap", "nye terapie",
                "ny vaksine", "nye vaksine", "vaksineutvikling", "utvikling av vaksin", 
                "nytt legemiddel", "nye legemid", "ny behandling"]
#We tried having "new" and "medicine"(++) in two separate term lists combined by AND, but it was noisy, hence use of phrases in termlist b2

termlist3_b3 = ["neglected tropical disease", 
                "african trypanosomiasis", "aids", "hiv", "appendicitis", "buruli ulcer", "chagas", "chikungunya", "dengue", "diarrheal disease", "diphteria", "dracunculiasis", "ebola", 
                "guinea-worm disease", "echinococcosis", "foodborne trematodiases", "hemolytic disease", "hepatitis B", "human african trypanosomiasis", "sleeping sickness", "leishmaniasis", "leprosy", 
                "lower respiratory infection", "respiratory tract infection", "lymphatic filariasis","malaria", 
                "maternal hemorrage", "maternal sepsis", "measles", "mycetom", "chromoblastomycosis", "deep mycoses", "neonatal encephalopathy", "neural tube defect",
                "onchocerciasis", "river blindness", "pertussis", "rabies", "rheumatic heart disease", "scabies", "schistosomiasis", "sickle cell", 
                "soil-transmitted helminthiasis", "hookworm", "roundworm", "whipworm", "ascaris lumbricoides",
                "trichuris trichiura", "necator americanus", "ancylostoma duodenale", "snakebite envenoming", "taeniasis", "cysticercosis", "tetanus", "trachoma", 
                "trichuriasis", "tuberculosis", "typhiod fever", "yaws", "yellow fever",

                "neglisjert tropesykdom", "neglisjerte tropesykdom", "neglisjert tropesjukdom", "neglisjerte tropesjukdom", 
                "afrikansk trypanosomiasis", "apendisitt", "blindtarmbetennelse", "burulisår", "diare", "difteri", "ekinokkokose", "trematodeinfeksjon",
                "hemolytisk", "hepatitt B", "lepra", "luftveisinfeksjon", "lymfatisk filariasis", "meslinger", "mykose", "kromomykose",
                "onkocerkose", "kikhoste", "skabb", "sigdcelle", 
                "helmintiasis", "jordoverført helminthiasis", "hakeorm", "rundorm", "guineaorm", "trichuris", "necator", "ancylostoma", 
                "taeniainfeksjon", "cysticerkose", "trakom", "tuberkulose", "tyfoid", "frambøsi", "gulfeber",

                "virus", "epidemi", "pandemi", "infectious", "communicable",
                "smittsom", "overførbar",
                ]
 #a few general terms ("virus", "epidemi" etc.) not originally included in the Web of Science were added to termlist3_b3 
 #as very few hits resulted from the title search when using only the names of specific diseases

#phrasedefault3_b1 = r'(?:{})'.format('|'.join(termlist3_b1))
phrasedefault3_b2 = r'(?:{})'.format('|'.join(termlist3_b2))
phrasedefault3_b3 = r'(?:{})'.format('|'.join(termlist3_b3))
```


```python
#Search 1 - in LMICs data
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_b2, na=False, case=False))
        & ((Data['LMICs']==True)|(Data['result_title'].str.contains(phrasedefault3_b3, na=False, case=False)))
    )
),"tempsdg03_b"] = "SDG03_b"

print("Number of results = ", len(Data[(Data.tempsdg03_b == "SDG03_b")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg03_b == "SDG03_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist3_b4 = ["doha declaration", "compulsory licens", "patent", "intellectual property", "TRIPS agreement",
                "doha-erklæring", "tvangslisens", "immaterielle rett", "intellektuell eiendom", "TRIPS-avtal"]

termlist3_b5 = ["pharmaceuticals", "medicine", "vaccine", "immunisation", "immunization", "essential drug", "medication", "treatment access", "access to therapy", 
                "legemid", "medisin", "medikament", "vaksine", "immunisering", "essensiell medisin", "livsnødvendig medisin", "behandlingstilgang", "tilgang til behandling", "adgang til behandling", "åtgang til behandling"]

termlist3_b6 = ["essential", "life saving", "life-saving", "emergency", "health", "medical",
                "essensiel", "livred", "livsviktig", "krise", "akutt", "helse", "medisinsk"]

termlist3_b7 = ["treatment", "therapy", 
                "behandling", "terapi"]

termlist3_b8 = ["access", "affordab", "low cost", "low-cost", "inexpensive", "free of charge", "expensive", 
                "tilgang", "adgang", "åtgang", "rimelig", "rimeleg", "billig", "billeg", "gratis"]

termlist3_b9 = ["vaccine equity", "vaccine inequit", 
                "vaksinefordeling", "fordeling av vaksiner"]

phrasedefault3_b4 = r'(?:{})'.format('|'.join(termlist3_b4))
phrasedefault3_b5 = r'(?:{})'.format('|'.join(termlist3_b5))
phrasedefault3_b6 = r'(?:{})'.format('|'.join(termlist3_b6))
phrasedefault3_b7 = r'(?:{})'.format('|'.join(termlist3_b7))
phrasedefault3_b8 = r'(?:{})'.format('|'.join(termlist3_b8))
phrasedefault3_b9 = r'(?:{})'.format('|'.join(termlist3_b9))
```


```python
#Search 1
# This search (vaccine equity OR trips/doha + medicines OR medicines + access) is wider than the WOS search (vaccine equity OR trips/doha AND medicines AND access) - adaptation to titles, where
# we were missing results about access in for certain countries. It adds a few noisy results about individual-level access to medicines (which are perhaps more relevant in 3.8 than 3.b).
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_b9, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault3_b4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_b5, na=False, case=False)))
    |
    (
        (
            (Data['result_title'].str.contains(phrasedefault3_b5, na=False, case=False)) 
            |((Data['result_title'].str.contains(phrasedefault3_b6, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_b7, na=False, case=False))) 
        )
        & (Data['result_title'].str.contains(phrasedefault3_b8, na=False, case=False))
    )
),"tempsdg03_b"] = "SDG03_b"

print("Number of results = ", len(Data[(Data.tempsdg03_b == "SDG03_b")])) 
```


```python
test=Data.loc[(Data.tempsdg03_b == "SDG03_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.c
*Substantially increase health financing and the recruitment, development, training and retention of the health workforce in developing countries, especially in least developed countries and small island developing States*

*Oppnå betydelig økt finansiering av helsetjenester og rekruttering, utvikling og opplæring av helsepersonell i utviklingsland, særlig i de minst utviklede landene og små utviklingsøystater, og arbeide for at slikt personell blir værende i landene*

#### Phrase 1


```python
#Termlists
termlist3_c1 = ["recruitment", "professional development", "retention", "capacity building", "capacity development", "train more", "recruit more", "increase trained",
                "increase the number of", "human capital flight", "brain drain", "emigration", "turnover", "intention to leave",
                
                "rekruttering", "fagutvikl", "faglig utvikl", "fagleg utvikl", "bevaring", "kapasitetsbygging", "kapasitetsutvikling", "trene fle", "rekruttere fle",
                "øke trente", "auke trente", "øke antallet", "øke tallet", "auke talet", "hjerneflukt", "emigrasjon", "utskifting", "gjennom"]

termlist3_c2 = ["increase", "improv", "enhanc", 
                "øk", "auk", "bedr", "betr", "styrk", "utvid"]

termlist3_c3 = ["training", "education",
                "trening", "opplæring", "utdanning"]

termlist3_c4 = ["health", "medical", 
                "helse", "medisinsk"]

termlist3_c5 = ["workforce", "professional", "worker", "personnel", "practitioner", "human resources", "student", 
                "arbeidsstyrke", "profesjonell", "arbeider", "arbeidar", "personell", "personale", "utøver", "utøvar", "menneskelige ressurs", "menneskelege ressurs"]

termlist3_c6 = ["nurse", "doctor", "physician", "anesthetist", "audiologist", "dental staff", "dentist", "doula", "emergency medical dispatcher", "health educator",
                "health facility administrator", "infection control practitioner", "medical chaperone", "medical laboratory personnel", "nutritionist",
                "therapist", "optometrist", "pharmacist", "allergist", "anesthesiolog", "cardiolog", "dermatolog", "endocrinolog", "gastroenterolog", "general practic",
                "geriatrician", "gynecologist", "hospitalist", "nephrolog", "neurolog", "oncolog", "ophtalmolog", "otolaryngolog", "midwives", "pathologist", "pediatric",
                "physiatrist", "pulmonolog", "radiolog", "rheumatolog", "surgeon", "urolog", 
                 
                "sykepleier", "sjukepleiar", "doktor", "lege", "anestesiolog", "anestesilege", "audiograf", "tannlege", "AMK-operatør", "smittevern", "laboratorieperson",
                "ernæringsfysiolog", "terapeut", "farmasøyt", "allergolog", "kardiolog", "endokrinolog", "allmennlege", "geriatrik", "gynekolog", "nevrolog", "onkolog", 
                "oftalmolog", "jordmor", "jordmødre", "patolog", "pediater", "kirurg"]                               

phrasedefault3_c1 = r'(?:{})'.format('|'.join(termlist3_c1))
phrasedefault3_c2 = r'(?:{})'.format('|'.join(termlist3_c2))
phrasedefault3_c3 = r'(?:{})'.format('|'.join(termlist3_c3))
phrasedefault3_c4 = r'(?:{})'.format('|'.join(termlist3_c4))
phrasedefault3_c5 = r'(?:{})'.format('|'.join(termlist3_c5))
phrasedefault3_c6 = r'(?:{})'.format('|'.join(termlist3_c6))
```


```python
#Search 1 - in LMICs data
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault3_c1, na=False, case=False))
            |((Data['result_title'].str.contains(phrasedefault3_c2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_c3, na=False, case=False)))
        )
        & 
        (
            ((Data['result_title'].str.contains(phrasedefault3_c4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_c5, na=False, case=False)))
            |(Data['result_title'].str.contains(phrasedefault3_c6, na=False, case=False))
        )    
    )
    & (Data['LMICs']==True)
),"tempsdg03_c"] = "SDG03_c"

print("Number of results = ", len(Data[(Data.tempsdg03_c == "SDG03_c")]))  
```

#### Phrase 2



```python
#Termlists
termlist3_c8 = ["financing", "investment", "investing", "fund", "health spending", "health care spending", "health budget", "public spending", "government spending",
                "financial assist", "economic assist", "financial support", "financial resources", "subsidy", "subsidies", "subsidis", "subsidiz",
                "cooperation fund", "development spending",

                "finansie", "fond", "helseutgift", "helsebudsjett", "offentlige utgifter", "offentlege utgifter", "finansiell assistanse", "økonomisk assistanse", 
                "finansiell støtte", "finansiell stønad", "finansielle ressurs", "subsidi", "offentlig utviklings", "offentleg utviklings", "offisiell utviklings", "samarbeidsfond"]

termlist3_c8_case = ["ODA", "invest", "Invest"]

termlist3_c9 = ["international", "development", "foreign", 
                "internasjonal", "utvikling", "utenlands", "utanlands"]

termlist3_c10 = ["aid", "assistance", "finance", "grant", 
                 "hjelp", "støtte", "stønad", "bistand", "assistanse", "finansie"]

termlist3_c11 = ["health sector", "health financing", "health budget", "health spending", "health service", "healthcare", "health care", "medical care",
                 "medical research", "health research", "health R&D", "medical R&D",
                 
                 "helsesektor", "helsefinansiering", "helsebudjett", "helseøkonomi", "helseutgift", "helsetjeneste", "helseteneste", "omsorgstjeneste", "omsorgsteneste", 
                 "medisinsk forskning", "medisinsk forsking", "helseforskning", "helseforsking"]

phrasedefault3_c8 = r'(?:{})'.format('|'.join(termlist3_c8))
phrasespecific3_c8_case = r'\b(?:{})\b'.format('|'.join(termlist3_c8_case))
phrasedefault3_c9 = r'(?:{})'.format('|'.join(termlist3_c9))
phrasedefault3_c10 = r'(?:{})'.format('|'.join(termlist3_c10))
phrasedefault3_c11 = r'(?:{})'.format('|'.join(termlist3_c11))
```


```python
#Search - in LMICs data
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_c8, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific3_c8_case, na=False, case=True))
        |((Data['result_title'].str.contains(phrasedefault3_c9, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_c10, na=False, case=False)))
    )
    & (Data['result_title'].str.contains(phrasedefault3_c11, na=False, case=False)) 
    & (Data['LMICs']==True)
),"tempsdg03_c"] = "SDG03_c"

print("Number of results = ", len(Data[(Data.tempsdg03_c == "SDG03_c")]))  
```


```python
test=Data.loc[(Data.tempsdg03_c == "SDG03_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.d
*Strengthen the capacity of all countries, in particular developing countries, for early warning, risk reduction and management of national and global health risks*

*Styrke kapasiteten i alle land, særlig i utviklingsland, for tidligvarsling, risikoredusering og håndtering av nasjonale og globale helserisikoer*


```python
#Termlists
termlist3_d1 = ["national health risk", "global health risk", "public health risk", 
                "pandemic preparedness", "pandemic polic", "epidemic", "outbreak", "medical disaster", "health emergenc", 
                "radiation emergenc", "radiation event", "chemical event", "chemical emergenc", "zoonotic event", "zoonotic emergenc", 
                "food safety", "foodborne event", "biosecurity event", "biosecurity emergenc",
                "antimicrobial resistan", "antibiotic resistan", "resistance to antibiotics", "antifungal resistan",
                
                "helserisiko", "epidemisk", "epidemier", "epidemien", "utbrudd", "utbrot", 
                "medisinsk katastrofe", 
                "strålingsulykke", "kjemikalieulykke", 
                "zoonotisk", "matsikkerhe", "matbåren", "biosikkerhe", 
                "antimikrobiell resistens", "antibiotikaresistens", "antimykotisk"]

termlist3_d1trunk = ["epidemi"]

termlist3_d2 = ["capacity", "early warning", "early detection", "surveillance", "monitoring system", "laboratory reporting", "laboratory infrastructure", "laboratory quality", "laboratory system",
                "preparing", "prepare", "disaster planning", "national health emergency framework", "emergency risk assessment", "risk reduction", "risk management", "risk communication",
                "emergency management", "emergency response", "personnel deployment", "security authorities", 
                "vaccination program", "vaccination framework", "immunisation program", "immunization program", 
                "legislation", "polic", "financing", "international health regulation", "national focal point", "national action plan",

                "kapasitet", "tidligvarsling", "tidlig varsling", "tidlegvarsling", "tidleg varsling", "tidlig oppdag", "tidleg oppdag", "overvåk", "overvaking", "laboratorie",
                "forberedt", "førebudd", "katastrofeplan", "kriseplan", "nasjonal helseberedskapsplan", "risikovurdering", "risikoreduksjon", "risikohåndtering", "risikokommunikasjon",
                "krisehåndtering", "kriserespons", "sikkerhetsmyndighet", "tryggingsorgan", 
                "vaksinasjonsprogram", "vaksinasjonsrammeverk", "immuniseringsprogram",
                "lovgivning", "lovgiving", "politikk", "retningslin", "finansiering", "internasjonalt helsereglement", "internasjonale helsereglement", "nasjonal handlingsplan"]

#termlist3_d3 = ["blight", "plant pathogen", "plant disease" ]       
# for a title search, it was not necessary to exlude the terms in termslist 3_d3 with a NOT search         

termlist3_d4 = ["pandemi"]

termlist3_d5 = ["influenza", "health", "hospital", "clinic", "ward", "care", "nurs", "pharmac", "medic", "vaccin",
                "influensa", "helse", "sykehus", "sjukehus", "avdeling", "klinikk", "omsorg", "farmas", "medisin", "vaksin"]

phrasedefault3_d1 = r'(?:{})'.format('|'.join(termlist3_d1))
phrasespecific3_d1trunk = r'\b(?:{})\b'.format('|'.join(termlist3_d1trunk))
phrasedefault3_d2 = r'(?:{})'.format('|'.join(termlist3_d2))
#phrasedefault3_d3 = r'(?:{})'.format('|'.join(termlist3_d3))
phrasedefault3_d4 = r'(?:{})'.format('|'.join(termlist3_d4))
phrasedefault3_d5 = r'(?:{})'.format('|'.join(termlist3_d5))
```


```python
#search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_d1, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific3_d1trunk, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault3_d4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_d5, na=False, case=False)))
    )
    & (Data['result_title'].str.contains(phrasedefault3_d2, na=False, case=False))
),"tempsdg03_d"] = "SDG03_d"

print("Number of results = ", len(Data[(Data.tempsdg03_d == "SDG03_d")])) 
```


```python
test=Data.loc[(Data.tempsdg03_d == "SDG03_d"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3 mentions


```python
#Termlists
termlist3_1 = ["SDG 3", "SDGs 3", "SDG3", "sustainable development goal 3", 
               "bærekraftsmål 3", "berekraftsmål 3"]
termlist3_2 = ["sustainable development goal", 
               "bærekraftsmål", "berekraftsmål"]
termlist3_3 = ["goal 3", 
               "mål 3"]
termlist3_4 = ["sustainable development goal", "SDG", "goal 3", 
               "bærekraftsmål", "berekraftsmål", "mål 3"]
termlist3_5 = ["health",
               "helse"]
termlist3_6 = ["good health and well-being", 
               "god helse og livskvalitet"]

phrasedefault3_1 = r'(?:{})'.format('|'.join(termlist3_1))
phrasedefault3_2 = r'(?:{})'.format('|'.join(termlist3_2))
phrasedefault3_3 = r'(?:{})'.format('|'.join(termlist3_3))
phrasedefault3_4 = r'(?:{})'.format('|'.join(termlist3_4))
phrasedefault3_5 = r'(?:{})'.format('|'.join(termlist3_5))
phrasedefault3_6 = r'(?:{})'.format('|'.join(termlist3_6))

```


```python
#search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault3_1, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault3_2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_3, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasedefault3_4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault3_5, na=False, case=False)))
    |(Data['result_title'].str.contains(phrasedefault3_6, na=False, case=False))
),"tempmentionsdg03"] = "SDG03"

print("Number of results = ", len(Data[(Data.tempmentionsdg03 == "SDG03")])) 
```


```python
test=Data.loc[(Data.tempmentionsdg03 == "SDG03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 4

### SDG 4.1
By 2030, ensure that all girls and boys complete free, equitable and quality primary and secondary education leading to relevant and effective learning outcomes

*Innen 2030 sikre at alle jenter og gutter fullfører gratis og likeverdig grunnskole og videregående opplæring av høy kvalitet som kan gi dem et relevant og reelt læringsutbytte*

#### Phrase 1


```python
#Termlists
termlist4_1_1a = ["complet", "school completion", "finish", "graduat",
                  "fullfør", "gjennomføring"]
                  
termlist4_1_1b = ["primary school", "elementary school", "primary educat", "middle school", "secondary school", "secondary education",
                  
                  "barnesk", "grunnskulen", "grunnskolen", "grunnutdann", "grunnopplæring", "ungdomssk", "vidaregåande skule", "videregående skole", "vidaregåande opplæring", "videregående opplæring",
                  "yrkesskule", "yrkesopplæring"]
                  
termlist4_1_1c = ["school", "education",
                  "skole", "skule", "utdann"]

termlist4_1_1d = ["boys", "girls", "kids", "child", "children",
                  "gut", "gutar", "gutter", "jente", "jenter", "barn", "born", "unge", "ungdom", "ungdommer", "ungdomar"]                  

termlist4_1_1e = ["skole", "skule"]     

phrasedefault4_1_1a = r'(?:{})'.format('|'.join(termlist4_1_1a))
phrasedefault4_1_1b = r'(?:{})'.format('|'.join(termlist4_1_1b))
phrasedefault4_1_1c = r'(?:{})'.format('|'.join(termlist4_1_1c))
phrasespecific4_1_1d = r'(?:{})\b'.format('|'.join(termlist4_1_1d))
phrasespecific4_1_1e = r'\b(?:{})'.format('|'.join(termlist4_1_1e))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_1_1a, na=False, case=False))
    & 
    (
        (Data['result_title'].str.contains(phrasedefault4_1_1b, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasespecific4_1_1e, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault4_1_1c, na=False, case=False)) & (Data['result_title'].str.contains(phrasespecific4_1_1d, na=False, case=False)))
    )
),"tempsdg04_01"] = "SDG04_01"

print("Number of results = ", len(Data[(Data.tempsdg04_01 == "SDG04_01")])) 
```


```python
test=Data.loc[(Data.tempsdg04_01 == "SDG04_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist4_1_2a = ["dropout", "drop-out", "drop out", "dropping out", "early school-leaving", 
                  "droppe ut", "dropper ut", "frafall", "fråfall", "falle ut"]
                 
termlist4_1_2b = ["primary school", "elementary school", "primary educat", "middle school", "secondary school", "secondary education",
                  
                  "barnesk", "grunnskulen", "grunnskolen", "grunnutdann", "grunnopplæring", "ungdomssk", "vidaregåande skule", "videregående skole", "vidaregåande opplæring", "videregående opplæring",
                  "yrkesskule", "yrkesopplæring"]
                
termlist4_1_2c = ["school", "education",
                  "skole", "utdann"]

termlist4_1_2d = ["boys", "girls", "kids", "child", "children",
                  "gut", "gutar", "gutter", "jente", "jenter", "barn", "born", "unge", "ungdom", "ungdommer", "ungdomar"]

termlist4_1_2e = ["quit"]
                 
termlist4_1_2f = ["skole", "skule"]
                 

phrasedefault4_1_2a = r'(?:{})'.format('|'.join(termlist4_1_2a))
phrasedefault4_1_2b = r'(?:{})'.format('|'.join(termlist4_1_2b))
phrasedefault4_1_2c = r'(?:{})'.format('|'.join(termlist4_1_2c))
phrasespecific4_1_2d = r'(?:{})\b'.format('|'.join(termlist4_1_2d))
phrasespecific4_1_2e = r'\b(?:{})'.format('|'.join(termlist4_1_2e))
phrasespecific4_1_2f = r'\b(?:{})'.format('|'.join(termlist4_1_2f))
```


```python
#Search 
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault4_1_2a, na=False, case=False)) 
        |(Data['result_title'].str.contains(phrasespecific4_1_2e, na=False, case=False))
    )
    & 
    (
        (Data['result_title'].str.contains(phrasedefault4_1_2b, na=False, case=False)) 
        |(Data['result_title'].str.contains(phrasespecific4_1_2f, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault4_1_2c, na=False, case=False)) & (Data['result_title'].str.contains(phrasespecific4_1_2d, na=False, case=False)))
    )
),"tempsdg04_01"] = "SDG04_01"

print("Number of results = ", len(Data[(Data.tempsdg04_01 == "SDG04_01")])) 
```


```python
test=Data.loc[(Data.tempsdg04_01 == "SDG04_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3
The structure from Topic search in WoS (access+school+free) is simplified here because of title search. 'Free' is not included in the search, in order not to lose relevant hits.



```python
#Termlists
termlist4_1_3a = ["access", "entry", "enroll", "admission", "admit",
                  "tilgang", "adgang", "tillating", "tillatelse", "løyve", "høve"]
            
termlist4_1_3b = ["primary school", "elementary school", "primary educat", "middle school", "secondary school", "secondary education",
                  
                  "barnesk", "grunnskule", "grunnskole", "grunnutdann", "grunnopplæring", "ungdomssk", 
                  "vidaregåande skule", "videregående skole", "vidaregåande opplæring", "videregående opplæring",
                  "yrkesskule", "yrkesopplæring"]                 

termlist4_1_3c = ["enter"]
#Turns off truncation to avoid "STUDENTER"(NO)

phrasedefault4_1_3a = r'(?:{})'.format('|'.join(termlist4_1_3a))
phrasedefault4_1_3b = r'(?:{})'.format('|'.join(termlist4_1_3b))
phrasespecific4_1_3c = r'\b(?:{})\b'.format('|'.join(termlist4_1_3c))
```


```python
#Search 
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault4_1_3a, na=False, case=False)) 
        |(Data['result_title'].str.contains(phrasespecific4_1_3c, na=False, case=False))
    )
    & (Data['result_title'].str.contains(phrasedefault4_1_3b, na=False, case=False))    
),"tempsdg04_01"] = "SDG04_01"

print("Number of results = ", len(Data[(Data.tempsdg04_01 == "SDG04_01")])) 
```


```python
test=Data.loc[(Data.tempsdg04_01 == "SDG04_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4


```python
#Termlists
termlist4_1_4a = ["basic", "fundamental", "minim", "core", "elementary",
                  "basis", "kjerne", "elementær", "grunnlegg"]
                
termlist4_1_4b = ["proficienc", "skill", "comprehen", "literac", "mathematic", "math", "maths", "numera",
                  "ferdigh", "dyktigh", "kyndigh", "dugleik", "forstå"] 
                
termlist4_1_4c = ["basisferdighe", "basiskompetanse", "kjerneferdighe", "kjernekompetanse"]
                         
termlist4_1_4d = ["reading", "mathematic", "math", "maths", "numera",
                  "regneferdigh", "rekneferdigh", "talforstå", "tallforstå", "talferdigh", "tallferdigh", "matematikk", "rekning", "regning"]

termlist4_1_4e = ["school", "student", "boys", "girls", "kids", "child", 
                  "skole", "skule", "gut", "jente", "born", "barn", "elever", "elevar" ]
                 
termlist4_1_4f = ["read",
                 "les"]
                                   
                 
phrasedefault4_1_4a = r'(?:{})'.format('|'.join(termlist4_1_4a))
phrasedefault4_1_4b = r'(?:{})'.format('|'.join(termlist4_1_4b))
phrasedefault4_1_4c = r'(?:{})'.format('|'.join(termlist4_1_4c))
phrasedefault4_1_4d = r'(?:{})'.format('|'.join(termlist4_1_4d))
phrasedefault4_1_4e = r'(?:{})'.format('|'.join(termlist4_1_4e))
phrasespecific4_1_4f = r'\b(?:{})'.format('|'.join(termlist4_1_4f))
```


```python
#Search 
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault4_1_4a, na=False, case=False)) 
            & 
            (
                (Data['result_title'].str.contains(phrasedefault4_1_4b, na=False, case=False)) 
                |(Data['result_title'].str.contains(phrasespecific4_1_4f, na=False, case=False))
            )
        )
        |(Data['result_title'].str.contains(phrasedefault4_1_4c, na=False, case=False))
    )
    & 
    (
        (Data['result_title'].str.contains(phrasedefault4_1_4d, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasespecific4_1_4f, na=False, case=False))
    )
    & (Data['result_title'].str.contains(phrasedefault4_1_4e, na=False, case=False))
),"tempsdg04_01"] = "SDG04_01"

print("Number of results = ", len(Data[(Data.tempsdg04_01 == "SDG04_01")]))
```


```python
test=Data.loc[(Data.tempsdg04_01 == "SDG04_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4.2
By 2030, ensure that all girls and boys have access to quality early childhood development, care and pre-primary education so that they are ready for primary education

*Innen 2030 sikre alle jenter og gutter mulighet for god tidlig utvikling og omsorg og tilgang til førskole, slik at de er forberedt på å begynne i grunnskolen*

#### Phrase 1


```python
#Termlists
termlist4_2_1a = ["access", "obstacle", "barrier", "hinder", "hindrance", "equit", 
                "tilgang", "adgang", "tilgjenge", "barrier", "hindring", "hinder", "hindre"]

termlist4_2_1b = ["early childhood care", "kindergarten", "pre-kindergarten", "nurser", "pre-primary education", "pre school education", "preschool education", "pre-school education", "ECEC",
                  "førsk", "barnehage", "tidlig utvikling", "tidleg utvikling"]

termlist4_2_1c = ["early childhood", "under five", "under-five"]

termlist4_2_1d = ["education"]

termlist4_2_1e = ["barnehagedekning", "barnehageplass", "tilbud om barnehage", "tilbod om barnehage", "barnehageopptak", "opptak i barnehage", "opptak til barnehage"]


phrasedefault4_2_1a = r'(?:{})'.format('|'.join(termlist4_2_1a))
phrasedefault4_2_1b = r'(?:{})'.format('|'.join(termlist4_2_1b))
phrasedefault4_2_1c = r'(?:{})'.format('|'.join(termlist4_2_1c))
phrasedefault4_2_1d = r'(?:{})'.format('|'.join(termlist4_2_1d))
phrasedefault4_2_1e = r'(?:{})'.format('|'.join(termlist4_2_1e))
```


```python
#Search 
Data.loc[(
    (          
        (Data['result_title'].str.contains(phrasedefault4_2_1a, na=False, case=False))
        & 
        (
            (Data['result_title'].str.contains(phrasedefault4_2_1b, na=False, case=False))
            |((Data['result_title'].str.contains(phrasedefault4_2_1c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_2_1d, na=False, case=False)))
        )
    )
    | (Data['result_title'].str.contains(phrasedefault4_2_1e, na=False, case=False))  
    ),"tempsdg04_02"] = "SDG04_02"

print("Number of results = ", len(Data[(Data.tempsdg04_02 == "SDG04_02")]))  
```


```python
test=Data.loc[(Data.tempsdg04_02 == "SDG04_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist4_2_2a = ["school ready", "school-ready", "school readiness", "school-readiness",
                "skolemoden", "skulemoden", "skulemogen"]

termlist4_2_2b = ["ready", "readiness", "prepared", "transition",
                 "moden", "mogen", "forberedt", "førebudd", "overgang"]

termlist4_2_2c = ["primary education", "primary school", "elementary school", "first grade", "1st grade",
                "første klass", "fyrste klass", "6-åring", "seksåring", "fyrsteklass", "førsteklass", "skole", "skule", "barnehage"]

termlist4_2_2d = ["development",
                "utvikling"]

termlist4_2_2e = ["child", "under-five", "early childhood",
                "barn", "tidlig barndom", "tidleg barndom"]

termlist4_2_2f= ["school entry", "start school", "start school",
                "skolestart", "skulestart"]

termlist4_2_2g = ["klar", "klare", "klår", "klåre"]

termlist4_2_2h = ["ungdomssk", "videregående", "vidaregåande", "høgskule", "høgskole", "universitet", "voksen", "vaksen", "arbeid", "jobb", "yrke"]
                
phrasedefault4_2_2a = r'(?:{})'.format('|'.join(termlist4_2_2a))
phrasedefault4_2_2b = r'(?:{})'.format('|'.join(termlist4_2_2b))
phrasedefault4_2_2c = r'(?:{})'.format('|'.join(termlist4_2_2c))
phrasedefault4_2_2d = r'(?:{})'.format('|'.join(termlist4_2_2f))
phrasedefault4_2_2e = r'(?:{})'.format('|'.join(termlist4_2_2e))
phrasedefault4_2_2f = r'(?:{})'.format('|'.join(termlist4_2_2f))
phrasespecific4_2_2g = r'\b(?:{})\b'.format('|'.join(termlist4_2_2g))
phrasedefault4_2_2h = r'(?:{})'.format('|'.join(termlist4_2_2h))
```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault4_2_2a, na=False, case=False)) 
        |
        (
            ((Data['result_title'].str.contains(phrasedefault4_2_2b, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_2_2g, na=False, case=False))) 
            & (Data['result_title'].str.contains(phrasedefault4_2_2c, na=False, case=False))
        )
        | 
        (
            (Data['result_title'].str.contains(phrasedefault4_2_2d, na=False, case=False)) 
            & (Data['result_title'].str.contains(phrasedefault4_2_2e, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault4_2_2f, na=False, case=False))
        )
    )
    &(~Data['result_title'].str.contains(phrasedefault4_2_2h, na=False, case=False))
),"tempsdg04_02"] = "SDG04_02"

print("Number of results = ", len(Data[(Data.tempsdg04_02 == "SDG04_02")])) 
```


```python
test=Data.loc[(Data.tempsdg04_02 == "SDG04_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4.3
By 2030, ensure equal access for all women and men to affordable and quality technical, vocational and tertiary education, including university

*Innen 2030 sikre kvinner og menn lik tilgang til god teknisk og yrkesfaglig opplæring og høyere utdanning, inkludert universitetsutdanning, til en overkommelig pris*

#### Phrase 1 & Phrase 2
Due to title search, phrase 1 and phrase 2 from WoS are here combined into one phrase. To a great extent, in WoS, the two phrases contain the same terms. We have included *Access* in termlist e) -  which is searched in AND-combination with termlist d) *University* - in order to include some more hits.



```python
#Termlists
termlist4_3_1a = ["access", "inclusion", "inclusiv", "equit", "equal", "afford", "barrier", "obstacle", "discriminat",
                  
                "tilgang", "tilgjenge", "adgang", "inkluder", "rettferdig", "rettvis",
                "ikkje råd", "ikke råd", "barrier", "hindring", "hinder", "diskrimin", "utesteng"]
                
termlist4_3_1c = ["higher education",
                  "høgare utdann", "høyere utdann", "universitetsutdann", "fagskul", "fagskol"]

termlist4_3_1d = ["universit", "college",
                  "høgskule", "høgskole", "høyskole"]

termlist4_3_1e = ["admission", "enrol", "access", 
                 "adgang", "tilgang", "tilgjenge", "immatrikuler", "opptak"]

termlist4_3_1f = ["technic", "vocation", "tertiar", "university", "postsecondary", "post secondary",
                  "teknisk", "tertiær", "fagskole", "fagskul", "yrkesfaglig", "yrkesfagleg", "yrkesutdann", "yrkesopplæring", "universitet"]

termlist4_3_1g = ["education", "training", "school", "learning",
                  "utdann", "skole", "skule", "læring"
                  ]

termlist4_3_1h = ["open access", "åpen tilgang", "open tilgang", "equals", "accession", "library", 
                  "bibliotek", "hospital", "sykehus", "sjukehus"]
                 #Noisy phrases, removed with NOT

phrasedefault4_3_1a = r'(?:{})'.format('|'.join(termlist4_3_1a))
phrasedefault4_3_1c = r'(?:{})'.format('|'.join(termlist4_3_1c))
phrasedefault4_3_1d = r'(?:{})'.format('|'.join(termlist4_3_1d))
phrasedefault4_3_1e = r'(?:{})'.format('|'.join(termlist4_3_1e))
phrasedefault4_3_1f = r'(?:{})'.format('|'.join(termlist4_3_1f))
phrasedefault4_3_1g = r'(?:{})'.format('|'.join(termlist4_3_1g))
phrasedefault4_3_1h = r'(?:{})'.format('|'.join(termlist4_3_1h))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_3_1a, na=False, case=False)) 
    &
    (
        (Data['result_title'].str.contains(phrasedefault4_3_1c, na=False, case=False)) 
        |((Data['result_title'].str.contains(phrasedefault4_3_1d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_3_1e, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault4_3_1f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_3_1g, na=False, case=False)))
    )
    & (~Data['result_title'].str.contains(phrasedefault4_3_1h, na=False, case=False))
),"tempsdg04_03"] = "SDG04_03"

print("Number of results = ", len(Data[(Data.tempsdg04_03 == "SDG04_03")])) 
```


```python
test=Data.loc[(Data.tempsdg04_03 == "SDG04_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists

termlist4_3_3a = ["inclusive", "inclusion", 
                  "inkluder"]

termlist4_3_3b = ["higher education",
                  "høgare utdann", "høyere utdann", "universitetsutdann", "høgskuleutdann", "høgskoleutdann", "tertiærutdann"]

phrasedefault4_3_3a = r'(?:{})'.format('|'.join(termlist4_3_3a))
phrasedefault4_3_3b = r'(?:{})'.format('|'.join(termlist4_3_3b))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_3_3a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_3_3b, na=False, case=False))
    ),"tempsdg04_03"] = "SDG04_03"

print("Number of results = ", len(Data[(Data.tempsdg04_03 == "SDG04_03")])) 
```


```python
test=Data.loc[(Data.tempsdg04_03 == "SDG04_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4.4
By 2030, substantially increase the number of youth and adults who have relevant skills, including technical and vocational skills, for employment, decent jobs and entrepreneurship

*Innen 2030 oppnå en betydelig økning i antall unge og voksne som har kompetanse, blant annet i tekniske fag og yrkesfag, som er relevant for sysselsetting, anstendig arbeid og entreprenørskap*

#### Phrase 1


```python
#Termlists
termlist4_4_1a = ["skill", "abilit", "competenc", "literac",
                  "ferdigh", "kompetanse", "dugleik", "dyktighe",   
                ]
#"skill" covers "upskill" and "reskill" etc.
              
termlist4_4_1b = ["employability", "employment", "decent job", "decent work", "entrepreneurship",
                 "ansettelse", "sysselset", "tilset", "anstendig arbeid", "anstendig jobb", "jobb", "entreprenørskap" ]

termlist4_4_1c = ["entrepreneurship education", "entrepreneur education", "entrepreneurial education"]

phrasedefault4_4_1a = r'(?:{})'.format('|'.join(termlist4_4_1a))
phrasedefault4_4_1b = r'(?:{})'.format('|'.join(termlist4_4_1b))
phrasedefault4_4_1c = r'(?:{})'.format('|'.join(termlist4_4_1c))
```


```python
#Search 
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault4_4_1a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_1b, na=False, case=False)))
    |(Data['result_title'].str.contains(phrasedefault4_4_1c, na=False, case=False))
),"tempsdg04_04"] = "SDG04_04"

print("Number of results = ", len(Data[(Data.tempsdg04_04 == "SDG04_04")]))  
```


```python
test=Data.loc[(Data.tempsdg04_04 == "SDG04_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist4_4_2a = ["unemploy", "underemploy", "out of work", "not in work", 
                  "arbeidsledig", "langtidsledig", "arbeidslau", "arbeidslø", "utan arbeid", "uten arbeid", "utan jobb", "uten jobb", "ikkje i arbeid", "ikke i arbeid"]
  
termlist4_4_2acaps = ["NEET", "NEETs"]
    
termlist4_4_2b = ["skill", " abilit", "employability", "competenc", "litera", 
                  "continuing education", "lifelong learning", "life long learning", "adult learning", "adult education", "training program", "vocational training", "new skills",
                  
                  "ferdigh", "kompetanse", "evne", "dugleik", "dyktighe", "kyndig", 
                  "videreutdanning", "vidareutdanning", "livslang læring", "voksenopplæring", "vaksenopplæring", "opplæringsprogram", "yrkesopplæring"]
#" ability" is used with a space before to avoid many works about "disability" which are not to do with training/skills

phrasedefault4_4_2a = r'(?:{})'.format('|'.join(termlist4_4_2a))
phrasespecific4_4_2acaps = r'\b(?:{})'.format('|'.join(termlist4_4_2acaps))
phrasedefault4_4_2b = r'(?:{})'.format('|'.join(termlist4_4_2b))
```


```python
#Search 
phrase4_4_2 = Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault4_4_2a, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_4_2acaps, na=False, case=False)))
    & (Data['result_title'].str.contains(phrasedefault4_4_2b, na=False, case=False))
    ),"tempsdg04_04"] = "SDG04_04"

print("Number of results = ", len(Data[(Data.tempsdg04_04 == "SDG04_04")])) 
```


```python
test=Data.loc[(Data.tempsdg04_04 == "SDG04_04"), ("result_id", "result_title")]
test.iloc[0:5, ] 
```

#### Phrase 3


```python
#Termlists
termlist4_4_3a = ["read", "writ", "comput", "literacy", "numeracy",
                  "lese", "skrive", "digital kompetanse", "digitale ferdigh", "tallferdighe", "talferdigh", "talforst", "tallforst", "regneferdigh", "rekneferdigh", "reknedugleik",
                  "basisferdigh", "grunnleggende ferdigh", "grunnleggjande ferdigh"
                 ]

termlist4_4_3b = ["basic technolog", "specialized", "specialised"]

termlist4_4_3c = ["skills", "knowledge"]

termlist4_4_3d = ["learn and adapt"]

termlist4_4_3e = ["listen", "communicat"]

termlist4_4_3f = ["skills", "effective"]

termlist4_4_3g = ["kommunikasjonsferdigh", "lytteferdigh", "lederferdigh", "leiarferdigh", "lederkompetanse", "leiarkompetanse", "jobbkompetanse"]

termlist4_4_3h = ["think creatively", "creative thinking", "solve problem", "problem-solv",
                  "problemlø"]

termlist4_4_3i = ["interact",
                  "samhandl", "samarbeid"]

termlist4_4_3j = ["co-work", "colleague",
                  "kollega"]

termlist4_4_3k = ["work",
                  "arbeid", "jobb"]

termlist4_4_3l = ["team", "group",
                  "gruppe"]

termlist4_4_3m = ["education", "professional development", "adult education", "adult learning", "lifelong learning", "life long learning", "employee development", "new skills",
                  "utdanning", "voksenopplæring", "vaksenopplæring", "livslang læring"]

termlist4_4_3n = ["leader"]


termlist4_4_3o = ["follow",
                  "følge", "følgje", "motta", "ta imot"]

termlist4_4_3p = ["supervi",
                  "veiled", "rettlei", "veglei"]

termlist4_4_3q = ["transfer",
                  "overførbar"]

termlist4_4_3r = ["skills",
                  "ferdigh"]

termlist4_4_3s = ["employability", "employable",
                  "ansettbar", "arbeidsevne", "syssels"]

phrasedefault4_4_3a = r'(?:{})'.format('|'.join(termlist4_4_3a))
phrasedefault4_4_3b = r'(?:{})'.format('|'.join(termlist4_4_3b))
phrasedefault4_4_3c = r'(?:{})'.format('|'.join(termlist4_4_3c))
phrasedefault4_4_3d = r'(?:{})'.format('|'.join(termlist4_4_3d))
phrasedefault4_4_3e = r'(?:{})'.format('|'.join(termlist4_4_3e))
phrasedefault4_4_3f = r'(?:{})'.format('|'.join(termlist4_4_3f))
phrasedefault4_4_3g = r'(?:{})'.format('|'.join(termlist4_4_3g))
phrasedefault4_4_3h = r'(?:{})'.format('|'.join(termlist4_4_3h))
phrasedefault4_4_3i = r'(?:{})'.format('|'.join(termlist4_4_3i))
phrasedefault4_4_3j = r'(?:{})'.format('|'.join(termlist4_4_3j))
phrasedefault4_4_3k = r'(?:{})'.format('|'.join(termlist4_4_3k))
phrasedefault4_4_3l = r'(?:{})'.format('|'.join(termlist4_4_3l))
phrasedefault4_4_3m = r'(?:{})'.format('|'.join(termlist4_4_3m))
phrasedefault4_4_3n = r'(?:{})'.format('|'.join(termlist4_4_3n))
phrasedefault4_4_3o = r'(?:{})'.format('|'.join(termlist4_4_3o))
phrasedefault4_4_3p = r'(?:{})'.format('|'.join(termlist4_4_3p))
phrasedefault4_4_3q = r'(?:{})'.format('|'.join(termlist4_4_3q))
phrasedefault4_4_3r = r'(?:{})'.format('|'.join(termlist4_4_3r))
phrasedefault4_4_3s = r'(?:{})'.format('|'.join(termlist4_4_3s))
```


```python
#Search 
Data.loc[(
    (
     (Data['result_title'].str.contains(phrasedefault4_4_3a, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault4_4_3b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3c, na=False, case=False)))
    |(Data['result_title'].str.contains(phrasedefault4_4_3d, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault4_4_3e, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3f, na=False, case=False)))
    |(Data['result_title'].str.contains(phrasedefault4_4_3g, na=False, case=False))
    |(Data['result_title'].str.contains(phrasedefault4_4_3h, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault4_4_3i, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3j, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasedefault4_4_3k, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3l, na=False, case=False)))
    |(Data['result_title'].str.contains(phrasedefault4_4_3m, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault4_4_3n, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3f, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasedefault4_4_3o, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3p, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasedefault4_4_3q, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3r, na=False, case=False)))
    )
    & (Data['result_title'].str.contains(phrasedefault4_4_3s, na=False, case=False))
),"tempsdg04_04"] = "SDG04_04"

print("Number of results = ", len(Data[(Data.tempsdg04_04 == "SDG04_04")])) 
```


```python
test=Data.loc[(Data.tempsdg04_04 == "SDG04_04"), ("result_id", "result_title")]
test.iloc[0:5, ] 
```

#### Phrase 4


```python
#Termlists
termlist4_4_4a = ["information and communication technology", "ICT", "vocational", "technical", "technolog", "comput", "data", "digital", "information",
                  "informasjonsteknologi", "IKT", "fagsk", "teknisk", "teknologi"]

termlist4_4_4b = ["skill", "competen", "literac",
                  "ferdigh", "kompetanse", "evne", "dugleik", "dyktigh"]

termlist4_4_4c = ["it-kompetanse", "it-ferdigh", "ikt-kompetanse", "ikt-ferdigh", "datakompetanse", "dataferdigh", "teknologikompetanse", "teknologiferdigh"]

termlist4_4_4d = ["employ", "job", "decent work",
                  "ansett", "sysselset", "tilset", "anstendig arbeid", "anstendig jobb", "jobbrelevan", "arbeidsrelevan", "yrkesrelevan"]
                  
phrasedefault4_4_4a = r'(?:{})'.format('|'.join(termlist4_4_4a))
phrasedefault4_4_4b = r'(?:{})'.format('|'.join(termlist4_4_4b))
phrasedefault4_4_4c = r'(?:{})'.format('|'.join(termlist4_4_4c))
phrasedefault4_4_4d = r'(?:{})'.format('|'.join(termlist4_4_4d))         
```


```python
#Search 
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault4_4_4a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_4b, na=False, case=False)))
        | (Data['result_title'].str.contains(phrasedefault4_4_4c, na=False, case=False))
    )
    & (Data['result_title'].str.contains(phrasedefault4_4_4d, na=False, case=False))
),"tempsdg04_04"] = "SDG04_04"

print("Number of results = ", len(Data[(Data.tempsdg04_04 == "SDG04_04")])) 
```


```python
test=Data.loc[(Data.tempsdg04_04 == "SDG04_04"), ("result_id", "result_title")]
test.iloc[0:5, ] 
```

### SDG 4.5
By 2030, eliminate gender disparities in education and ensure equal access to all levels of education and vocational training for the vulnerable, including persons with disabilities, indigenous peoples and children in vulnerable situations

*Innen 2030 avskaffe kjønnsforskjeller i utdanning og opplæring og sikre lik tilgang til alle nivåer innenfor utdanning og yrkesfaglig opplæring for sårbare grupper, inkludert personer med nedsatt funksjonsevne, urfolk og barn i utsatte situasjoner*

#### Phrase 1


```python
#Termlists
termlist4_5_1a = ["gender", "girl", "woman", "women", "female", "boy", "male",
                "kjønn", "jente", "kvinne", "gut"]

termlist4_5_1b = ["equit", "equal", "balanc",
                  "rettferd", "rettvis", "jevnbyrdig", "likheit", "likhet", "likskap", "ulikskap", "skilnad", "balans"]

termlist4_5_1c = ["likestilling"]

termlist4_5_1d = ["school", "educat", "vocational training", "student",
                  "skole", "skule", "utdann", "undervisning", "undervising", "opplæring", "yrkesfag"]

phrasedefault4_5_1a = r'(?:{})'.format('|'.join(termlist4_5_1a))
phrasedefault4_5_1b = r'(?:{})'.format('|'.join(termlist4_5_1b))
phrasedefault4_5_1c = r'(?:{})'.format('|'.join(termlist4_5_1c))
phrasedefault4_5_1d = r'(?:{})'.format('|'.join(termlist4_5_1d))
```


```python
#Search 
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault4_5_1a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_5_1b, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault4_5_1c, na=False, case=False))
    )
    & (Data['result_title'].str.contains(phrasedefault4_5_1d, na=False, case=False))
),"tempsdg04_05"] = "SDG04_05"

print("Number of results = ", len(Data[(Data.tempsdg04_05 == "SDG04_05")])) 
```


```python
test=Data.loc[(Data.tempsdg04_05 == "SDG04_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist4_5_2a = ["gender", "girl", "woman", "women", "female", "boy", "male",
                  "kjønn", "jente", "kvinne", "gut"]

termlist4_5_2b = ["non-equit", "non-equal", "inequal", "unequal", "unbalanc", "imbalanc", "disparit", "discriminat", "obstacle", "barrier", "hindrance", "hinder", "bias", "parity", "gap",
                  "ulikhet", "ulikheit", "urett", "ubalans", "misforhold", "forskjell", "skilnad", "diskriminer", "hinder", "hindre", "barrier"]

termlist4_5_2c = ["gender gap", "gender parity",
                  "kjønnsdiskriminering", "kjønnsforskjell", "kjønnsskilnad"]

termlist4_5_2d = ["school", "educat", "vocational training", "student",
                  "skole", "skule", "utdann", "undervisning", "undervising", "opplæring", "yrkesfag"]

termlist4_5_2e = ["mortality", "health", "wealth"]

termlist4_5_2f = ["difference", "discrepan",
                  "forskjell", "ulik", "skilnad"]

termlist4_5_2g = ["complet", "result", "perform", "success", "achieve", "access", "enter", "entry", "enroll", "admission", "admit", "graduation", "graduating", "attend",
                  "fullfør", "gjennomfør", "resultat", "suksess", "oppnå", "adgang", "opptak", "tilgang"]

phrasedefault4_5_2a = r'(?:{})'.format('|'.join(termlist4_5_2a))
phrasedefault4_5_2b = r'(?:{})'.format('|'.join(termlist4_5_2b))
phrasedefault4_5_2c = r'(?:{})'.format('|'.join(termlist4_5_2c))
phrasedefault4_5_2d = r'(?:{})'.format('|'.join(termlist4_5_2d))
phrasedefault4_5_2e = r'(?:{})'.format('|'.join(termlist4_5_2e))
phrasedefault4_5_2f = r'(?:{})'.format('|'.join(termlist4_5_2f))
phrasedefault4_5_2g = r'(?:{})'.format('|'.join(termlist4_5_2g))
```


```python
#Search
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault4_5_2c, na=False, case=False))
            |
            (
                (Data['result_title'].str.contains(phrasedefault4_5_2a, na=False, case=False)) 
                &
                (
                    (Data['result_title'].str.contains(phrasedefault4_5_2b, na=False, case=False))
                    |((Data['result_title'].str.contains(phrasedefault4_5_2f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_5_2g, na=False, case=False)))
                )
            )
        )
        & (Data['result_title'].str.contains(phrasedefault4_5_2d, na=False, case=False))
    )
    & (~Data['result_title'].str.contains(phrasedefault4_5_2e, na=False, case=False))
),"tempsdg04_05"] = "SDG04_05"

print("Number of results = ", len(Data[(Data.tempsdg04_05 == "SDG04_05")]))  
```


```python
test=Data.loc[(Data.tempsdg04_05 == "SDG04_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3

Here under terms for vulnerable groups we have included Norwegian-specific indigenous and minority groups (source: Utdanningsdirektoratet (n.d.) Nasjonale minoriteter. https://www.udir.no/laring-og-trivsel/nasjonale-minoriteter/hva-er-en-nasjonal-minoritet/ (accessed Nov 2022))).


```python
#Termlists
termlist4_5_3a = ["access", "admission", "admit", "attend", "entry", "enrol", "inclusion", "inclusiv", "non-discriminat", "equitab",
                  "education for all", "Rights of Persons with Disabilities", "CRPD",
                  
                  "tilgang", "tilgjenge", "adkomst", "adgang", "opptak", "inkluder", "rettferd", "rettvis", 
                  "utdanning for alle", "rettigheter til personer med nedsatt funksjonsevne", "rettar til menneske med nedsett funksjonsevne"]

termlist4_5_3b = ["discriminat", "non-discriminat", "inequit", "unequit", "disparit", "barrier", "obstacle", "exclusion", "excluding",
                  "diskriminer", "urettvis", "urettferd", "barrier", "hinder", "hindr", "eksklu"]

termlist4_5_3c =  ["school", "educat", "vocational training",
                  "skole", "skule", "utdann", "undervis", "opplæring", "yrkesfagl"]

termlist4_5_3d =  ["person", "people", "adult", "child", "student", "youth", "adolescent",
                   "menneske", "vaksne", "voksne", "elev", "ung", "tenåring", "barn", "born"]

termlist4_5_3e = ["disabled", "disabilit", "unemployed", "older", "elderly", "poor", "poverty", "disadvantaged", "vulnerab", "displaced", "marginali", "developing countr",
                  "specific learning disabilit", "SLD", "other health impairment", "autism spectrum disorder", "ASD", "emotional disturbance", "speech impairment",
                  "language impairment", "visual impairment", "blindness", "deafness", "hearing impairment", "deaf-blindness", "orthopedic impairment", "intellectual disabilit", "traumatic brain injur", "multiple disabilit",
                  
                  "uføre", "funksjonshem", "arbeidsl", "utan arbeid", "uten arbeid", "fattig", "lavinntekt", "låginntekt", "lav inntekt", "låg inntekt", "sårbar", "diskriminert",
                  "marginalisert", "utviklingsland", "u-land", "lærevansk", "særskilte behov", "autismespekter", "emosjonelle forstyrr", "talevansk", "språkvansk", "synsvansk", "blind", "døv", "hørsel",
                  "ortopediske vansk", "intellektuelle vansk", "traumatisk hjerneskade"]
                  #Norwegian terms for OLDER are not included as they cause noise.

termlist4_5_3f = ["disab", "disadvantage", "vulnerab", "indigenous", "the poor",
                  "refugee", "asylum", "displaced", "migrant", 
                  "low income", "minorit", "marginal", "slum", "rural", "special educational needs",
                  "LGBT", "lesbian", "gay", "bisexual", "transgender", 
                  
                  "uføre", "funksjonshem", "sårbar", "hjemløs", "heimlaus", "urfolk", "urbefolkning", "urinnvån", "minoritet",
                  "sápmi", "sami", "minoritet", "jøder", "jødar", "kvener", "kvenar", "norskfinn", "skogfinn", "romani", "tatere", "taterar",
                  "asylsøk", "flyktning", "innvandr",
                  "fattig", "lavinntekt", "låg inntekt", "låginntekt", "lav inntekt", 
                  "transperson", "lesbisk", "homofile", "homoseksuell", "bifil", "lbht", "interkjønn", "innfød"]

termlist4_5_3g = ["special educat", "special needs educat", "inclusive education", "aided education",
                  "tilrettelagt undervisning", "spesialundervisning", "tilpasset opplæring", "tilpassa opplæring", "inkluderende opplæring", "inkluderande opplæring"]

termlist4_5_3h = ["SEN"]

phrasedefault4_5_3a = r'(?:{})'.format('|'.join(termlist4_5_3a))
phrasedefault4_5_3b = r'(?:{})'.format('|'.join(termlist4_5_3b))
phrasedefault4_5_3c = r'(?:{})'.format('|'.join(termlist4_5_3c))
phrasedefault4_5_3d = r'(?:{})'.format('|'.join(termlist4_5_3d))
phrasedefault4_5_3e = r'(?:{})'.format('|'.join(termlist4_5_3e))
phrasedefault4_5_3f = r'(?:{})'.format('|'.join(termlist4_5_3f))
phrasedefault4_5_3g = r'(?:{})'.format('|'.join(termlist4_5_3g))
phrasespecific4_5_3h = r'\b(?:{})\b'.format('|'.join(termlist4_5_3h))
```


```python
#Search 
Data.loc[(
    (
        (
            ((Data['result_title'].str.contains(phrasedefault4_5_3a, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault4_5_3b, na=False, case=False)))
            & (Data['result_title'].str.contains(phrasedefault4_5_3c, na=False, case=False))
        )
        &
        (
            ((Data['result_title'].str.contains(phrasedefault4_5_3d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_5_3e, na=False, case=False)))
            |(Data['result_title'].str.contains(phrasedefault4_5_3f, na=False, case=False)) 
            |(Data['result_title'].str.contains(phrasespecific4_5_3h, na=False, case=True))
        )
    )
    |
    (
        ((Data['result_title'].str.contains(phrasedefault4_5_3a, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault4_5_3b, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault4_5_3g, na=False, case=False))
    )
),"tempsdg04_05"] = "SDG04_05"

print("Number of results = ", len(Data[(Data.tempsdg04_05 == "SDG04_05")]))
```


```python
test=Data.loc[(Data.tempsdg04_05 == "SDG04_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4.6
By 2030, ensure that all youth and a substantial proportion of adults, both men and women, achieve literacy and numeracy

*Innen 2030 sikre at all ungdom og en betydelig andel voksne, både kvinner og menn, lærer å lese, skrive og regne*

#### Phrase 1
The phrase is simplified compared to topic search in WoS. The structure of the search is *skills + reading/mathematics*.



```python
#Termlists                
termlist4_6_1a = ["proficienc", "skill", "comprehension", "comprehend", "literac",
                  "ferdigh", "dyktighe", "kyndighe", "kompetanse", "evne", "dugleik", "forstå", "nivå", "grunnlegg"]

termlist4_6_1b = ["ability", "abilities", "level"]

termlist4_6_1c =  ["reading", "literate", "mathematic", "maths", "mathematics", "numera", 
                   
                   "leseferdigh", "leseforstå", "lesekompetanse", "lesedugleik",
                   "rekne", "rekna", "regneferdigh", "rekneferdigh", "reknedugleik",
                   "talforstå", "tallforstå", "talferdigh", "tallferdigh", "matematikk"]

termlist4_6_1d = ["read", 
                  "lese", "lesa", "lesing", "rekning", "regning"]                 

termlist4_6_1e = ["teacher", "readability", "readiness", "spread", "information literacy",
                  "lærer", "lærar", "student", "skille", "mikropolitisk"] #Noisy terms, removed with NOT

termlist4_6_1f = ["core literacy", "functional literacy", "basic literacy"]

phrasedefault4_6_1a = r'(?:{})'.format('|'.join(termlist4_6_1a))
phrasespecific4_6_1b = r'\b(?:{})\b'.format('|'.join(termlist4_6_1b))
phrasedefault4_6_1c = r'(?:{})'.format('|'.join(termlist4_6_1c))
phrasespecific4_6_1d = r'\b(?:{})\b'.format('|'.join(termlist4_6_1d))
phrasedefault4_6_1e = r'(?:{})'.format('|'.join(termlist4_6_1e))
phrasedefault4_6_1f = r'(?:{})'.format('|'.join(termlist4_6_1f))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_6_1f, na=False, case=False))
    |
    (
        (
             ((Data['result_title'].str.contains(phrasedefault4_6_1a, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_6_1b, na=False, case=False)))
             & ((Data['result_title'].str.contains(phrasedefault4_6_1c, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_6_1d, na=False, case=False)))
        )
    & (~Data['result_title'].str.contains(phrasedefault4_6_1e, na=False, case=False))
    )
),"tempsdg04_06"] = "SDG04_06"

print("Number of results = ", len(Data[(Data.tempsdg04_06 == "SDG04_06")]))
```


```python
test=Data.loc[(Data.tempsdg04_06 == "SDG04_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist4_6_2 = ["illiterate child", "illiterate people", "illiterate user", 
                 "analfabet", "analphabet", "innumeracy", "innumerate",
                 
                 "analfabet", "lesekyn", "lesekunnig", "talkyn", "tallkyn", "talkunn", "talforståing", "tallforståelse"] 

termlist4_6_2a = ["illitera"] 
                         
phrasedefault4_6_2 = r'\b(?:{})'.format('|'.join(termlist4_6_2))
phrasedefault4_6_2a = r'(?:{})'.format('|'.join(termlist4_6_2a))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_6_2, na=False, case=False))   
    |
    (
        (Data['result_title'].str.contains(phrasedefault4_6_2a, na=False, case=False)) 
        & ((Data['result_title'].str.contains(phrasedefault4_6_1c, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_6_1d, na=False, case=False)))
    )
),"tempsdg04_06"] = "SDG04_06"

print("Number of results = ", len(Data[(Data.tempsdg04_06 == "SDG04_06")]))
```


```python
test=Data.loc[(Data.tempsdg04_06 == "SDG04_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4.7
By 2030, ensure that all learners acquire the knowledge and skills needed to promote sustainable development, including, among others, through education for sustainable development and sustainable lifestyles, human rights, gender equality, promotion of a culture of peace and non-violence, global citizenship and appreciation of cultural diversity and of culture’s contribution to sustainable development

*Innen 2030 sikre at alle elever og studenter tilegner seg den kompetansen som er nødvendig for å fremme bærekraftig utvikling, blant annet gjennom utdanning i bærekraftig utvikling og livsstil, menneskerettigheter, likestilling, fremme av freds- og ikkevoldskultur, globalt borgerskap og verdsetting av kulturelt mangfold og kulturens bidrag til bærekraftig utvikling*

#### Phrase 1


```python
#Termlists
termlist4_7_1a = ["educat", "curricul", "student assess", "teaching", "teacher education", "teacher training", "online learning", "professional learning", 
                  "utdann", "opplæring", "pensum", "studieplan", "emneplan", "fagplan", "studentvurdering", "elevvurdering", "undervisning", "undervising", "nettbasert læring", "online læring", "profesjonslæring"]  
                  
termlist4_7_1b = ["learn",
                  "læring"]

termlist4_7_1c = ["vurdering"]

termlist4_7_1d =  ["student",
                   "elev"]  
                 
termlist4_7_1e = ["sustainable development", "sustainable lifestyle", "global citizen", "glocal", "human right", "gender equality", 
                  "peace", "non-violen", "cultural divers", "toleran",
                  
                  "bærekraftig utvikling", "berekraftig utvikling", "berekraftig livsstil", "bærekraftig livsstil", 
                  "global borg", "globalt borg", "menneskerett", "likestilling", "ikkje-vald", "ikke-vold", "ikkevold", "ikkjevald", 
                  "kulturelt mangfold", "kulturelt mangfald"]
                  
termlist4_7_1f = ["sustainability",
                  "bærekraft", "berekraft"]

termlist4_7_1g = ["interdisciplinar", "transdisciplinar", "crossdisciplinar", "cultural", "economic", "ecological", "participation", 
                  "agency", "responsibility", "ethic", "wicked problem", 
                  "complexity", "capacity for change", "transition",
                  
                  "tverrfagl", "tverrvit", "kulturell", "økonomisk", "økologisk", "deltak", "handling", "ansvar", "etisk", 
                  "kompleks", "uløselig problem", "uløyseleg problem", "endring", "overgang"]
                  
      
termlist4_7_1h = ["Global Citizenship Education"]
                  
termlist4_7_1i = ["fred"]

phrasedefault4_7_1a = r'(?:{})'.format('|'.join(termlist4_7_1a))
phrasedefault4_7_1b = r'(?:{})'.format('|'.join(termlist4_7_1b))
phrasedefault4_7_1c = r'(?:{})'.format('|'.join(termlist4_7_1c))
phrasedefault4_7_1d = r'(?:{})'.format('|'.join(termlist4_7_1d))
phrasedefault4_7_1e = r'(?:{})'.format('|'.join(termlist4_7_1e))
phrasedefault4_7_1f = r'(?:{})'.format('|'.join(termlist4_7_1f))
phrasedefault4_7_1g = r'(?:{})'.format('|'.join(termlist4_7_1g))
phrasedefault4_7_1h = r'(?:{})'.format('|'.join(termlist4_7_1h))
phrasespecific4_7_1i = r'\b(?:{})'.format('|'.join(termlist4_7_1i))
```


```python
#Search 
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault4_7_1a, na=False, case=False)) 
        |((Data['result_title'].str.contains(phrasedefault4_7_1b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_7_1d, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault4_7_1c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_7_1d, na=False, case=False)))
    )
    &
    (
        (Data['result_title'].str.contains(phrasedefault4_7_1e, na=False, case=False))
        | (Data['result_title'].str.contains(phrasespecific4_7_1i, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault4_7_1f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_7_1g, na=False, case=False)))
        | (Data['result_title'].str.contains(phrasedefault4_7_1h, na=False, case=False)) 
    )
),"tempsdg04_07"] = "SDG04_07"

print("Number of results = ", len(Data[(Data.tempsdg04_07 == "SDG04_07")])) 
```


```python
test=Data.loc[(Data.tempsdg04_07 == "SDG04_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist4_7_2a = ["education for sustainab", "education in sustainab", "education on sustainab", "sustainable development education", "sustainability education",
                  
                  "utdanning for bærekraft", "utdanning for berekraft", "utdanning for en bærekraft", "utdanning for ei berekraft",
                  "opplæring for bærekraft", "opplæring for berekraft", "opplæring for en bærekraft", "opplæring for ei berekraft"
                 ]
                  

termlist4_7_2b = ["whole school", "teaching",
                  
                  "heilhetlig", "heilskapleg", "helhetlig", "helskole", "heilskule",
                  "undervisning", "undervising", "utdanning", "opplæring"]

termlist4_7_2c = ["sustainab", "berekraft", "bærekraft"]

termlist4_7_2cspec = ["ESD", "UBU"]

termlist4_7_2d = ["educat", "utdann", "opplæring"]
 

phrasedefault4_7_2a = r'(?:{})'.format('|'.join(termlist4_7_2a))
phrasedefault4_7_2b = r'(?:{})'.format('|'.join(termlist4_7_2b))
phrasedefault4_7_2c = r'(?:{})'.format('|'.join(termlist4_7_2c))
phrasedespecific4_7_2c = r'\b(?:{})\b'.format('|'.join(termlist4_7_2cspec))
phrasedefault4_7_2d = r'(?:{})'.format('|'.join(termlist4_7_2d))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_7_2a, na=False, case=False)) 
    | 
    (
        (Data['result_title'].str.contains(phrasedefault4_7_2b, na=False, case=False))
        & ((Data['result_title'].str.contains(phrasedefault4_7_2c, na=False, case=False)) | (Data['result_title'].str.contains(phrasedespecific4_7_2c, na=False, case=True)))
        & (Data['result_title'].str.contains(phrasedefault4_7_2d, na=False, case=False))
    )
),"tempsdg04_07"] = "SDG04_07"

print("Number of results = ", len(Data[(Data.tempsdg04_07 == "SDG04_07")])) 
```


```python
test=Data.loc[(Data.tempsdg04_07 == "SDG04_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist4_7_3a = ["culture", "cultural",
                  "kultur"]
                                
termlist4_7_3b = ["sustainable development",
                  "bærekraft", "berekraft"]

termlist4_7_3c = ["kulturøkonomi", "kulturskole", "kulturskule"]

phrasespecific4_7_3a = r'\b(?:{})'.format('|'.join(termlist4_7_3a))
phrasedefault4_7_3b = r'(?:{})'.format('|'.join(termlist4_7_3b))
phrasedefault4_7_3c = r'(?:{})'.format('|'.join(termlist4_7_3c))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasespecific4_7_3a, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault4_7_3b, na=False, case=False))      
    & (~Data['result_title'].str.contains(phrasedefault4_7_3c, na=False, case=False))
),"tempsdg04_07"] = "SDG04_07"

print("Number of results = ", len(Data[(Data.tempsdg04_07 == "SDG04_07")])) 
```


```python
test=Data.loc[(Data.tempsdg04_07 == "SDG04_07"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

### SDG 4.a
Build and upgrade education facilities that are child, disability and gender sensitive and provide safe, non-violent, inclusive and effective learning environments for all

*Etablere og oppgradere utdanningstilbud som er barnevennlige, og som ivaretar hensynet til kjønnsforskjeller og til personer med nedsatt funksjonsevne og sikrer trygge, ikke-voldelige, inkluderende og effektive læringsmiljø for alle*

#### Phrase 1


```python
#Termlists
termlist4_a_1a = ["school", "education facilit",
                  "skole", "skule", "opplæring"]
                 
termlist4_a_1b = ["safe", "secure", "non-violen", "inclusive", 
                  "sikker", "sikre", "trygg", "barneven", "borneven", "ikke-vold", "ikkje-vald", "inkluder"]

termlist4_a_1c =  ["sensitiv",
                   "følsom", "hensyn", "omsyn"]

termlist4_a_1d = ["child", "disability", "gender",
                  "barn", "born", "funksjonshem", "funksjonsevne", "kjønn"]

termlist4_a_1e = ["taste sensitivity", "smak"]

phrasedefault4_a_1a = r'(?:{})'.format('|'.join(termlist4_a_1a))
phrasedefault4_a_1b = r'(?:{})'.format('|'.join(termlist4_a_1b))
phrasedefault4_a_1c = r'(?:{})'.format('|'.join(termlist4_a_1c))
phrasedefault4_a_1d = r'(?:{})'.format('|'.join(termlist4_a_1d))
phrasedefault4_a_1e = r'(?:{})'.format('|'.join(termlist4_a_1e))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_a_1a, na=False, case=False))
    &
    (
        (Data['result_title'].str.contains(phrasedefault4_a_1b, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault4_a_1c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_a_1d, na=False, case=False)))     
    )
    & (~Data['result_title'].str.contains(phrasedefault4_a_1e, na=False, case=False))
),"tempsdg04_a"] = "SDG04_0a"

print("Number of results = ", len(Data[(Data.tempsdg04_a == "SDG04_0a")]))
```


```python
test=Data.loc[(Data.tempsdg04_a == "SDG04_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2
Here we have chosen a more simple search than in WoS. *Effective* is not included here. The structure here is then *Learning environment + School.*


```python
#Termlists
termlist4_a_2a = ["learning environment", "indoor environmental quality", "air quality",
                  "læringsmiljø", "inneklima"]

termlist4_a_2b =  ["primary school", "elementary school", "primary educat", "middle school", "secondary school", "secondary educat", "school", "education", "learner", "classroom",
                   "skole", "skule", "utdann", "opplæring", "lærling", "klasserom"]

termlist4_a_2c = ["student", "universit", "higher education", "teacher education", 
                  "høyere utdanning", "høgare utdanning", "lærerutdanning", "lærarutdanning"]

phrasedefault4_a_2a = r'(?:{})'.format('|'.join(termlist4_a_2a))
phrasedefault4_a_2b = r'(?:{})'.format('|'.join(termlist4_a_2b))
phrasedefault4_a_2c = r'(?:{})'.format('|'.join(termlist4_a_2c))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_a_2a, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault4_a_2b, na=False, case=False)) 
    & (~Data['result_title'].str.contains(phrasedefault4_a_2c, na=False, case=False))
),"tempsdg04_a"] = "SDG04_0a"

print("Number of results = ", len(Data[(Data.tempsdg04_a == "SDG04_0a")]))
```


```python
test=Data.loc[(Data.tempsdg04_a == "SDG04_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3
The structure from topic search in WoS is a bit simplified. *Access* is  not included, and the structure here is: *School + Basic services*


```python
#Termlists
termlist4_a_3a = ["school", "education", "skole", "skule", "opplæring", "utdanning"]

termlist4_a_3b = ["basic services", "basic facilities", "basic infrastructure",
                  "electricity", "electrical supply", "modern energy", "internet facilities", "computer facilities", "ICT facilit",
                  "adapted infrastructure", "adapted material",
                  "universal design", "drinking water", "sanitation", "handwash", "hand wash", "WASH facilities", "toilet",

                  "grunnleggende tjenester", "grunnleggjande tenester",
                  "elektrisitet", "fasilitet", "infrastruktur",
                  "universell design", "universell utforming",
                  "drikkeva", "sanitær", "håndvask", "handvask", "vaskemuligh", "vaskemog", "toalett"
                 ]

termlist4_a_3c = ["higher education"]

phrasedefault4_a_3a = r'(?:{})'.format('|'.join(termlist4_a_3a))
phrasedefault4_a_3b = r'(?:{})'.format('|'.join(termlist4_a_3b))
phrasedefault4_a_3c = r'(?:{})'.format('|'.join(termlist4_a_3c))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_a_3a, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault4_a_3b, na=False, case=False))
    & (~Data['result_title'].str.contains(phrasedefault4_a_3c, na=False, case=False))
),"tempsdg04_a"] = "SDG04_0a"

print("Number of results = ", len(Data[(Data.tempsdg04_a == "SDG04_0a")]))
```


```python
test=Data.loc[(Data.tempsdg04_a == "SDG04_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4.b
By 2020, substantially expand globally the number of scholarships available to developing countries, in particular least developed countries, small island developing States and African countries, for enrolment in higher education, including vocational training and information and communications technology, technical, engineering and scientific programmes, in developed countries and other developing countries

*Innen 2020 oppnå en vesentlig økning globalt i antall stipender som er tilgjengelige for studenter fra utviklingsland, særlig de minst utviklede landene, små utviklingsøystater og afrikanske land, for å gi dem tilgang til høyere utdanning, blant annet yrkesfaglig opplæring og programmer for informasjons- og kommunikasjonsteknologi, teknikk, ingeniørfag og vitenskap, både i andre utviklingsland og i utviklede land*


```python
#Termlists
termlist4_ba = ["scholarships", "scholarship program", "fellowship", "exchange program", 
                "student exchange", "student mobility", "study abroad", "overseas stud",

                "stipend", "økonomisk støtte", "utveksling", "legat"]
                   
termlist4_bbuntrunc = ["grant", "grants"]

termlist4_bc = ["sponsor"]

termlist4_bd = ["education", "student", "trainee", "mobility", "utdanning"]         

phrasedefault4_ba = r'(?:{})'.format('|'.join(termlist4_ba))
phrasespecific4_bbuntrunc = r'\b(?:{})\b'.format('|'.join(termlist4_bbuntrunc))
phrasedefault4_bc = r'(?:{})'.format('|'.join(termlist4_bc))
phrasedefault4_bd = r'(?:{})'.format('|'.join(termlist4_bd))
```


```python
#Search
Data.loc[(
     (
         (Data['result_title'].str.contains(phrasedefault4_ba, na=False, case=False)) 
         |
         (
             ((Data['result_title'].str.contains(phrasespecific4_bbuntrunc, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault4_bc, na=False, case=False)))
             & (Data['result_title'].str.contains(phrasedefault4_bd, na=False, case=False))
         )
     )
    & (Data['LMICs']==True)
),"tempsdg04_b"] = "SDG04_b"

print("Number of results = ", len(Data[(Data.tempsdg04_b == "SDG04_b")]))  
```


```python
test=Data.loc[(Data.tempsdg04_b == "SDG04_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4.c
By 2030, substantially increase the supply of qualified teachers, including through international cooperation for teacher training in developing countries, especially least developed countries and small island developing States

*Innen 2030 oppnå en vesentlig økning i antall kvalifiserte lærere, blant annet gjennom internasjonalt samarbeid om lærerutdanning i utviklingsland, særlig i de minst utviklede landene og i små utviklingsøystater*

#### Phrase 1


```python
#Termlists
termlist4_c_1a = ["teacher supply", "supply of teacher", "teacher coverage", "teacher recruit", "recruitment of teacher", "recruiting of teacher", 
                 "lack of teacher", "teacher turnover", "teacher shortage", "teacher retention", "teacher attrition",
                  
                 "lærerdekning", "lærardekning", "lærerrekruttering", "lærarrekruttering", "rekruttering av lær", 
                 "lærermangel", "lærarmangel", "lærarturnover", "lærerturnover", "turnover av lær", 
                 "lærerslitasje", "lærarslitasje"
                ]

termlist4_c_1b = ["avgang", "slitasje", "mangel", "rekruttering"]

termlist4_c_1c = ["lærer", "lærar"]

termlist4_c_1d = ["barnehage"]
              
phrasedefault4_c_1a = r'(?:{})'.format('|'.join(termlist4_c_1a))
phrasespecific4_c_1b = r'\b(?:{})\b'.format('|'.join(termlist4_c_1b))
phrasedefault4_c_1c = r'(?:{})'.format('|'.join(termlist4_c_1c))
phrasedefault4_c_1d = r'(?:{})'.format('|'.join(termlist4_c_1d))
```


```python
#Search 
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault4_c_1a, na=False, case=False)) 
        | ((Data['result_title'].str.contains(phrasespecific4_c_1b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_c_1c, na=False, case=False)))
    )
    & (~Data['result_title'].str.contains(phrasedefault4_c_1d, na=False, case=False))
),"tempsdg04_c"] = "SDG04_c"

print("Number of results = ", len(Data[(Data.tempsdg04_c == "SDG04_c")]))
```


```python
test=Data.loc[(Data.tempsdg04_c == "SDG04_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist4_c_2a = ["teacher training", "teacher education", "education of teacher", "teacher qualification", "qualified teacher", "teacher student", 
                  
                  "lærarutdann", "lærerutdann", "utdanning av lærarar", "utdanning av lærere", "lærarstudent", "lærerstudent", 
                  "kvalifiserte lær", "lærarkompetanse", "lærerkompetanse", "lærerkvalifikasjon", "lærarkvalifikasjon"]
          
termlist4_c_2b = ["lærer", "lærar", "teacher"]

termlist4_c_2c = ["kvalifikasjon", "kvalifiser", "kompetanse", 
                  "qualification", "qualified", "training",]

phrasedefault4_c_2a = r'(?:{})'.format('|'.join(termlist4_c_2a))
phrasedefault4_c_2b = r'(?:{})'.format('|'.join(termlist4_c_2b))
phrasedefault4_c_2c = r'(?:{})'.format('|'.join(termlist4_c_2c))
```


```python
#Search 
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault4_c_2a, na=False, case=False)) 
        | ((Data['result_title'].str.contains(phrasedefault4_c_2b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_c_2c, na=False, case=False)))
    )
    & (Data['LMICs']==True)
),"tempsdg04_c"] = "SDG04_c"

print("Number of results = ", len(Data[(Data.tempsdg04_c == "SDG04_c")]))
```


```python
test=Data.loc[(Data.tempsdg04_c == "SDG04_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 4 mentions


```python
#Termlists

termlist_sdg4_a = ["SDG 4", "SDGs 4", "SDG4", "sustainable development goal 4", 
                  "bærekraftsmål 4", "berekraftsmål 4", "berekraftmål 4"]

termlist_sdg4_b = ["sustainable development goal",
                 "bærekraftsmål", "berekraftsmål", "berekraftmål"]
                 
termlist_sdg4_c = ["goal 4",
                   "mål 4"]

termlist_sdg4_d = ["education",
                  "utdann", "opplæring", "undervisning", "undervising"]
                  
termlist_sdg4_e = ["sustainable development goal", "SDG", "goal 4", 
                 "bærekraftsmål", "berekraftsmål", "berekraftmål", "mål 4"]

termlist_sdg4_f = ["learning", "teaching", "teacher", "early childhood", "child development", 
                  "education for sustainable", "global citizenship education", "transdisciplinary education", 
                  "inclusive education", "formal education", "primary education", "secondary education", "tertiary education", 
                  "higher education", "right to education", "access to education",  "education for all",  "education sector", 
                   
                   "utdann", "opplæring", "skolegang", "skulegang", "tidleg barndom", "tidlig barndom", 
                   "barns utvikling", "borns utvikling"]

termlist_sdg4_g = ["quality education", "god utdanning"]

phrase_sdg4_a = r'(?:{})'.format('|'.join(termlist_sdg4_a))
phrase_sdg4_b = r'(?:{})'.format('|'.join(termlist_sdg4_b))
phrase_sdg4_c = r'(?:{})'.format('|'.join(termlist_sdg4_c))
phrase_sdg4_d = r'(?:{})'.format('|'.join(termlist_sdg4_d))
phrase_sdg4_e = r'(?:{})'.format('|'.join(termlist_sdg4_e))
phrase_sdg4_f = r'(?:{})'.format('|'.join(termlist_sdg4_f))
phrase_sdg4_g = r'(?:{})'.format('|'.join(termlist_sdg4_g))
```


```python
#Search 
Data.loc[(
      (Data['result_title'].str.contains(phrase_sdg4_a, na=False, case=False))
      |((Data['result_title'].str.contains(phrase_sdg4_b, na=False, case=False)) & (Data['result_title'].str.contains(phrase_sdg4_c, na=False, case=False)))
      |((Data['result_title'].str.contains(phrase_sdg4_d, na=False, case=False)) & (Data['result_title'].str.contains(phrase_sdg4_e, na=False, case=False)))
      |((Data['result_title'].str.contains(phrase_sdg4_e, na=False, case=False)) & (Data['result_title'].str.contains(phrase_sdg4_f, na=False, case=False)))
      |(Data['result_title'].str.contains(phrase_sdg4_g, na=False, case=False))
),"tempmentionsdg04"] = "SDG04"
    
print("Number of results = ", len(Data[(Data.tempmentionsdg04 == "SDG04")])) 
```


```python
test=Data.loc[(Data.tempmentionsdg04 == "SDG04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 7

### SDG 7.1

*By 2030, ensure universal access to affordable, reliable and modern energy services*

*Innen 2030 sikre allmenn tilgang til pålitelige og moderne energitjenester til en overkommelig pris*

#### Phrase 1


```python
#Term lists
termlist7_1a = ["energy transition", 
                "energiomlegging", "energiomstilling"]

termlist7_1b = ["household", "cooking", "stove", "lighting", "lamps", "heating",
                "hushold", "hushald", "matlaging", "komfyr", "ovn", "lys", "lampe", "oppvarming"]

termlist7_1c = ["clean fuel", "clean energy", "clean electricity", "clean cooking", "clean stove", "clean lighting", "clean lamp", "clean heating",
                "modern fuel", "modern stove", "modern lighting", "modern lamps", "modern heating",
                
                "rent brennstoff", "reint brennstoff", "rentbrennende", "reintbrennande", "ren energi", "rein energi", "ren strøm", "rein straum", "ren elektrisitet", "rein elektrisitet"]

termlist7_1d = ["household", "homes", "house", "housing", "residential", "dwelling", "domestic", "slum", "village", "women", 
                "hushold", "hushald", "hjem", "heim", "hus", "bolig", "bustad", "landsby", "kvinne"]                                       

phrasedefault7_1a = r'(?:{})'.format('|'.join(termlist7_1a))
phrasedefault7_1b = r'(?:{})'.format('|'.join(termlist7_1b))
phrasedefault7_1c = r'(?:{})'.format('|'.join(termlist7_1c))
phrasedefault7_1d = r'(?:{})'.format('|'.join(termlist7_1d))
```


```python
#Search 7_1abcd - 
Data.loc[(
      (
          (
            (Data['result_title'].str.contains(phrasedefault7_1a, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault7_1b, na=False, case=False))    
          )     
       |(Data['result_title'].str.contains(phrasedefault7_1c, na=False, case=False)) 
      )
    & (Data['result_title'].str.contains(phrasedefault7_1d, na=False, case=False)) 
),"tempsdg07_01"] = "SDG07_01"

print("Number of results = ", len(Data[(Data.tempsdg07_01 == "SDG07_01")])) 
```


```python
test=Data.loc[(Data.tempsdg07_01 == "SDG07_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Term lists
termlist7_1e = ["solar cook", "solar box cook", "improved cookstove", "improved stove", "modern cookstove", "modern stove",
                "solkok", "solovn", "solcelleovn", "solfyr", "solgrill"]

phrasedefault7_1e = r'(?:{})'.format('|'.join(termlist7_1e))
```


```python
#Search 7_1e
Data.loc[(
 (Data['result_title'].str.contains(phrasedefault7_1e, na=False, case=False)) 
),"tempsdg07_01"] = "SDG07_01"

print("Number of results = ", len(Data[(Data.tempsdg07_01 == "SDG07_01")])) 
```


```python
test=Data.loc[(Data.tempsdg07_01 == "SDG07_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Term lists
termlist7_1f = ["kerosene", "solid fuel.*", "coal",
                "parafin.*", "fast bren.*", "koks"]
termlist7_1f2 = ["kerosene", "solid fuel.*",
                 "parafin.*", "fast bren.*", "koks"]

termlist7_1g = ["household", "home", "hous", "residential", "dwelling", "domestic use", "slum", "residential heating", "central heating", "winter heating",
                "cooking", "stove", "lighting", "lamps",

                "hushold", "hushald", "hjem", "heim", "hus", "bolig", "bustad", "slum",
                "oppvarming", "varme", "fyre", "fyring", "matlaging", "ovn", "lys", "belysning", "ljos", "lampe"]
                #There is no Norwegian translation of the search term "coal" as it only returns noise, not really a common fuel in Norway        

termlist7_1g2 = ["heating"]
    
phrasespecific7_1f = r'\b(?:{})\b'.format('|'.join(termlist7_1f))
phrasespecific7_1f2 = r'\b(?:{})\b'.format('|'.join(termlist7_1f2))
phrasedefault7_1g = r'(?:{})'.format('|'.join(termlist7_1g))
phrasedefault7_1g2 = r'(?:{})'.format('|'.join(termlist7_1g2))
```


```python
#Search 7_1fg
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasespecific7_1f, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault7_1g, na=False, case=False)) 
    )
    |
    (
        (Data['result_title'].str.contains(phrasespecific7_1f2, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault7_1g2, na=False, case=False)) 
    )
),"tempsdg07_01"] = "SDG07_01"

print("Number of results = ", len(Data[(Data.tempsdg07_01 == "SDG07_01")])) 
```


```python
test=Data.loc[(Data.tempsdg07_01 == "SDG07_01"), ("result_id", "result_title")]
test.iloc[0:8, ]
```

#### Phrase 4



```python
#Term lists
termlist7_1h = ["energy poverty", "energy vulnerability", "fuel poverty", "energy democracy", "energy justice", "energy inequit", "energy security", "energy insecur",
                "energifattigdom", "energisårbarhet", "energidemokrati", "energirettferdighet", "energisikkerhet"] 

phrasedefault7_1h = r'(?:{})'.format('|'.join(termlist7_1h))
```


```python
#Search 7_1h
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault7_1h, na=False, case=False)) 
),"tempsdg07_01"] = "SDG07_01"

print("Number of results = ", len(Data[(Data.tempsdg07_01 == "SDG07_01")]))  
```


```python
test=Data.loc[(Data.tempsdg07_01 == "SDG07_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 5



```python
#Term lists - 
termlist7_1i = ["electricity", "energy", "power", "universal electrification", "rural electrification", "national electrification", "electrification", "grid extension", "grid extensions",
                "access to energy", "provision of energy", "energy provision", "provision of electricity", "electricity provision", "electricity supply", "electrical supply", "power supply",
                
                "elektrisitet", "strøm", "straum", "energi", "kraft", "elektrifisering", "elektrisering", "mikronett", "øydrift", "tilgang til energi", "tilgang på energi", "energitilgang",
                "tilgang til elektrisitet", "tilgang på elektrisitet", "tilgang til strøm", "tilgang til straum", "tilgang på strøm", "tilgang på straum"]

termlist7_1j = ["household", "home", "house", "housing", "residential", "dwelling", "domestic use", "slum", "village","sustainable", "green", "clean","modern",
                "hushold", "hushald", "hjem", "heim", "hus", "bolig", "bustad", "slum", "landsby","bærekraftig", "berekraftig", "grøn", "ren", "rein", "moderne"]

termlist7_1k = ["rural", "remote region", "remote area", "remote communit",
                "landlig", "landsby"]

termlist7_1i2 = ["universal electrification", "rural electrification", "national electrification",
                 "elektrifisering"]

termlist7_1x = ["access", "provision",
                "tilgang", "tilbud", "tilbod"]

termlist7_1xt = ["energy services", "energy supply",
                 "energitjeneste", "energiteneste", "energiforsyning", "strømforsyning", "straumforsyning", "kraftforsyning"]

termlist7_1xtr = ["electric", "energy", "power",
                  "elektris", "energi", "kraft"]

termlist7_1xtra = ["electrification", "grid extension",
                   "elektrifiser"]

termlist7_1xtras = ["energy", "electricity", "electrical supply", "power supply",
                    "elektris", "energi", "strømforsyning", "straumforsyning", "kraftforsyning"]

phrasedefault7_1i = r'(?:{})'.format('|'.join(termlist7_1i))
phrasedefault7_1j = r'(?:{})'.format('|'.join(termlist7_1j))
phrasedefault7_1k = r'(?:{})'.format('|'.join(termlist7_1k))
phrasedefault7_1i2 = r'(?:{})'.format('|'.join(termlist7_1i2))
phrasedefault7_1x = r'(?:{})'.format('|'.join(termlist7_1x))
phrasedefault7_1xt = r'(?:{})'.format('|'.join(termlist7_1xt))
phrasedefault7_1xtr = r'(?:{})'.format('|'.join(termlist7_1xtr))
phrasedefault7_1xtra = r'(?:{})'.format('|'.join(termlist7_1xtra))
phrasedefault7_1xtras = r'(?:{})'.format('|'.join(termlist7_1xtras))
```


```python
#Search 1 - in LMICs data
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault7_1i2, na=False, case=False))
    |
    (
        (Data['result_title'].str.contains(phrasedefault7_1x, na=False, case=False))
        &
        (
            (Data['result_title'].str.contains(phrasedefault7_1xt, na=False, case=False))
            |((Data['result_title'].str.contains(phrasedefault7_1xtr, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_1j, na=False, case=False)))
        )
    )
    |
    (
        (
            (Data['result_title'].str.contains(phrasedefault7_1xtra, na=False, case=False))
            |((Data['result_title'].str.contains(phrasedefault7_1x, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_1xtras, na=False, case=False)))
        )
        & ((Data['LMICs']==True)|(Data['result_title'].str.contains(phrasedefault7_1k, na=False, case=False)))
    )
),"tempsdg07_01"] = "SDG07_01"
```


```python
print("Number of results = ", len(Data[(Data.tempsdg07_01 == "SDG07_01")])) 
```


```python
test=Data.loc[(Data.tempsdg07_01 == "SDG07_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 6


```python
#Term lists
termlist7_1l = ["stable", "stability", "reliable", "reliability", "secur", "resilient", "resilience", "affordable", "affordability", "inexpensive", "low cost", "cheap",
                "unstable", "instability", "unreliable", "unreliability", "unaffordable", "costly", "energy cost", "expensive",
                
                "stabil", "pålitelig", "påliteleg", "sikker", "robust", "rimelig", "rimeleg", "billig", "ustabil", "upålitelig", "upåliteleg", "kostbar", "dyr"]

termlist7_1m = ["energy services", "electric supply",
                "energitjeneste", "energiteneste", "energiforsyning", "strømforsyning", "straumforsyning", "kraftforsyning"]

termlist7_1n = ["energy", "power", "electricity",
                "energi", "strøm", "straum", "kraft", "elektrisitet"]

termlist7_1o = ["household", "home", "house", "housing", "residential", "dwelling", "domestic use", "slum", "village", "sustainable",
                "hushold", "hushald", "hjem", "heim", "hus", "bolig", "bustad", "slum", "landsby", "bærekraftig", "berekraftig",
                "forsyningssikkerhet", "forsyningssikkerheit"]

termlist7_1p = ["microgrid", "micro grid", "minigrid", "mini grid", "off grid solution", "off-grid system",
                "mikronett", "øydrift"]

termlist7_1q = ["energy", "electricity",
                "energi", "elektrisitet", "strøm", "straum", "kraft"]

termlist7_1r = ["infrastructure", "off grid", "decentralised", "decentralized", "cooperative",
                "infrastruktur", "desentralisert", "kooperativ"]

termlist7_1s = ["community energy", "community renewable energy",
                "energisamfunn"]

phrasedefault7_1l = r'(?:{})'.format('|'.join(termlist7_1l))
phrasedefault7_1m = r'(?:{})'.format('|'.join(termlist7_1m))
phrasedefault7_1n = r'(?:{})'.format('|'.join(termlist7_1n))
phrasedefault7_1o = r'(?:{})'.format('|'.join(termlist7_1o))
phrasedefault7_1p = r'(?:{})'.format('|'.join(termlist7_1p))
phrasedefault7_1q = r'(?:{})'.format('|'.join(termlist7_1q))
phrasedefault7_1r = r'(?:{})'.format('|'.join(termlist7_1r))
phrasedefault7_1s = r'(?:{})'.format('|'.join(termlist7_1s))
```


```python
#Search 7_1lmnopqrs
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault7_1l, na=False, case=False))
    &
    (
        (Data['result_title'].str.contains(phrasedefault7_1m, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_1n, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_1o, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault7_1p, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_1q, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_1r, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault7_1s, na=False, case=False))
    )
),"tempsdg07_01"] = "SDG07_01"

print("Number of results = ", len(Data[(Data.tempsdg07_01 == "SDG07_01")]))  
```


```python
test=Data.loc[(Data.tempsdg07_01 == "SDG07_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 7.2

*By 2030, increase substantially the share of renewable energy in the global energy mix*

*Innen 2030 øke andelen fornybar energi i verdens samlede energiforbruk betydelig*

#### Phrase 1


```python
# Term lists
termlist7_2a = ["renewable",
                "fornybar"]

termlist7_2b = ["energy transition", "sector transformation", "energy transformation",
                "omstilling", "endring", "transform"]

termlist7_2c = ["renewable energy",
                "fornybar energi"]

termlist7_2d = ["substitut", "uptake",
                "erstat", "overgang"]

phrasedefault7_2a = r'(?:{})'.format('|'.join(termlist7_2a))
phrasedefault7_2b = r'(?:{})'.format('|'.join(termlist7_2b))
phrasedefault7_2c = r'(?:{})'.format('|'.join(termlist7_2c))
phrasedefault7_2d = r'(?:{})'.format('|'.join(termlist7_2d))
```


```python
#Search 7_2abcd
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault7_2a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2b, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasedefault7_2c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2d, na=False, case=False)))   
),"tempsdg07_02"] = "SDG07_02"

print("Number of results = ", len(Data[(Data.tempsdg07_02 == "SDG07_02")])) 
```


```python
test=Data.loc[(Data.tempsdg07_02 == "SDG07_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2



```python
# Term lists
termlist7_2c = ["relian", "primary use", "primary usage", "primary source", "adopt", "implementation", "uptake", "contribution", "proportion", "share", "expansion", "feasibility", 
                "attractiveness", "incentive", "initiative", "affordab", "inexpensive", "low cost", "economic viability", "cost-effectiveness", 
                "cost-advantage", "investment", "investing", "investor", "subsidies", "subsidisation", "subsidization", "financing", "funding", 
                "commercialisation", "commercialization", "energy service", "energy sector", "generation", "capacity", "global energy", 
                "global electricity", "energy mix", "market share", "barrier", "obstacle", "implement", "incentivi", "energy transition", 
                "renewable transition", "transition to", "energy certificat", "green certificat", "policy", "policies", "legislation", "kyoto protocol",
                "strateg", "energy management", "energy planning", "subsidise", "subsidize", "green bond", "climate bond" "feed-in tariff", "upscale", "scale-up", 
                "commercial development", "development commercially", "roll out", "rollout", "sustainable development", "sustainable energy development",

                "avhengig", "primær bruk", "primærbruk", "primær kilde", "primær kjelde", "primærkilde", "primærkjelde", "ta i bruk", "implementer", "oppfat", 
                "bidra", "utvid", "gjennomfør", "attraktiv", "insentiv", "initiativ", "rimelig", "rimeleg", "billig", "billeg", "lav kost", "låg kost", 
                "kostnadseffektiv", "invester", "subsidie", "finansiering", "kommersialisering", "energitjeneste", "energiteneste", "energisektor", "produksjon",
                "kapasitet", "global energi", "global elektrisitet", "energimiks", "markedsandel", "marknadsdel", 
                "barriere", "hinder", "hindring", "energiomstilling", "omstilling til fornybar", "overgang", "fornybar", 
                "elsertifi", "grønn sertifi", "grøn sertifi", "politikk", "retningslin", "lovgiv", "lovgjev", "kyotoprotokollen", "kyotoavtalen", 
                "energiledelse", "energileiing", "energiplanlegging", "invester", "grønne obligasjon", "grøne obligasjon", "klimaobligasjon",
                "innmatingstariff", "oppskaler", "kommersiell utvikling", "lanser", "rulle ut", "utrulling", 
                "bærekraftig utvikling", "berekraftig utvikling", "bærekraftig energiutvikling", "berekraftig energiutvikling"]
termlist7_2ctrunk = ["invest", 
                     "andel", "andeler", "del"]                
termlist7_2d = ["non conventional energy", 
                "alternativ energi"]
termlist7_2e = ["electricity", "power", "energy", 
                "elektrisitet", "kraft", "strøm", "straum", "energi"]
termlist7_2f = ["renewable", "sustainable", "green", "hydrothermal", "geothermal", "hydroelectric", "hydropower", "hydro", "hydrokinetic",
                "fornybar", "bærekraftig", "berekraftig", "grøn", "hydroterm", "varmekraft", "geoterm", "hydroelektris", "vannkraft", "vasskraft", "hydrokinetisk"]
termlist7_2g = ["geothermal heat pump", "ground source heat pump", "solar cell", "solar-cell", "solar panel", "solar-panel", "solar power", "solar array", "solar PV", 
                "photovoltaic", "solar energy collector", "solar farm", "solar plant", "solar park", "solar district heating", "solar district cooling", 
                "solar air heating system", "solar space heating system", 
                "varmepumpe", "solcelle", "solkraft", "solenergi", "fotovoltaisk", "solfang", "solsaml", "solvarm", "solpark", "solcellepark"] 
termlist7_2h = ["solar thermal", 
                "sol", "solvarme"]
termlist7_2i = ["power", "technolog", "collector", "district", 
                "kraft", "teknologi", "saml", "distrikt"]
termlist7_2j = ["solar thermal energy", 
                "solenergi", "solvarm"]
termlist7_2k = ["power", "electric", "water heating", "industrial process heat", 
                "kraft", "elektris", "vann", "vass", "spillvarme"]              
termlist7_2l = ["wind farm", "wind turbine", "wind park", "wind factory", "wind factories", "wind energy",
                "tidal turbine", "stream turbine", "current turbine", "tidal power", "tidal energy", "marine energy",
                "vindkraftverk", "vindturbin", "vindpark", "vindmøllepark", "havvind", "vindenergi",
                "tidevannsturbin", "havstrømturbin", "tidevannskraft", "tidevannsenergi", "marin energi", "havenergi"]
termlist7_2m = ["wave energy", 
                "bølgeenergi", "bølgjeenergi", "bølgekraft", "bølgjekraft"]              
termlist7_2n = ["converter", "renewable", "power", "generat", "energy harvesting", 
                "omdann", "omform", "konverter", "fornybar", "kraft", "energi"] 
termlist7_2o = ["biofuel", "bioenergy", "biodiesel", 
                "biodrivstoff", "bioenergi"]
termlist7_2p = ["biomass", "wind", "solar", "ammonia", 
                "vind", "sol"]
termlist7_2q = ["electric", "energy", "power system",
                "elektrisk", "energi", "kraftsystem"]
termlist7_2r = ["hydrogen"]
termlist7_2s = ["renewable", "green", 
                "fornybar", "bærekraft", "berekraft", "grøn"]
termlist7_2t = ["fuel cell", "battery", "batteries", "lithium ion", "energy storage", "smart grid", "smart-grid",
                "brenselcelle", "brenselscelle", "brenslecelle", "batteri", "litium-ion", "energilagring", "smartgrid", "smartnett"]
termlist7_2u = ["renewab", "sustainab", 
                "fornybar", "bærekraft", "berekraft"]

phrasedefault7_2c = r'(?:{})'.format('|'.join(termlist7_2c))
phrasespecific7_2c = r'\b(?:{})\b'.format('|'.join(termlist7_2ctrunk))
phrasedefault7_2d = r'(?:{})'.format('|'.join(termlist7_2d))
phrasespecific7_2e = r'\b(?:{})'.format('|'.join(termlist7_2e))
phrasedefault7_2f = r'(?:{})'.format('|'.join(termlist7_2f))
phrasedefault7_2g = r'(?:{})'.format('|'.join(termlist7_2g))
phrasedefault7_2h = r'(?:{})'.format('|'.join(termlist7_2h))
phrasedefault7_2i = r'(?:{})'.format('|'.join(termlist7_2i))
phrasedefault7_2j = r'(?:{})'.format('|'.join(termlist7_2j))
phrasedefault7_2k = r'(?:{})'.format('|'.join(termlist7_2k))
phrasedefault7_2l = r'(?:{})'.format('|'.join(termlist7_2l))
phrasedefault7_2m = r'(?:{})'.format('|'.join(termlist7_2m))
phrasedefault7_2n = r'(?:{})'.format('|'.join(termlist7_2n))
phrasedefault7_2o = r'(?:{})'.format('|'.join(termlist7_2o))
phrasedefault7_2p = r'(?:{})'.format('|'.join(termlist7_2p))
phrasedefault7_2q = r'(?:{})'.format('|'.join(termlist7_2q))
phrasedefault7_2r = r'(?:{})'.format('|'.join(termlist7_2r))
phrasedefault7_2s = r'(?:{})'.format('|'.join(termlist7_2s))
phrasedefault7_2t = r'(?:{})'.format('|'.join(termlist7_2t))
phrasedefault7_2u = r'(?:{})'.format('|'.join(termlist7_2u))
```


```python
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault7_2c, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific7_2c, na=False, case=False))) 
    &
    (
        (Data['result_title'].str.contains(phrasedefault7_2d, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasespecific7_2e, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2f, na=False, case=False)))
        | (Data['result_title'].str.contains(phrasedefault7_2g, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault7_2h, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2i, na=False, case=False)))
        | ((Data['result_title'].str.contains(phrasedefault7_2j, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2k, na=False, case=False)))  
        | (Data['result_title'].str.contains(phrasedefault7_2l, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault7_2m, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2n, na=False, case=False)))
        | (Data['result_title'].str.contains(phrasedefault7_2o, na=False, case=False)) 
        | ((Data['result_title'].str.contains(phrasedefault7_2p, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2q, na=False, case=False)))  
        | ((Data['result_title'].str.contains(phrasedefault7_2r, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2s, na=False, case=False)))   
        | ((Data['result_title'].str.contains(phrasedefault7_2t, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_2u, na=False, case=False)))  
    )
),"tempsdg07_02"] = "SDG07_02"

print("Number of results = ", len(Data[(Data.tempsdg07_02 == "SDG07_02")]))  
```


```python
test=Data.loc[(Data.tempsdg07_02 == "SDG07_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
# Term lists
termlist7_2m = ["fossil fuel", "natural gas", "grey hydrogen", "conventional energy",
                "fossilt brensel", "fossile brensl", "fossilt brennstoff", "fossile brennstoff", "naturgass", "grått hydrogen", "konvensjonell energi"]
termlist7_2mtrunk = ["coal", "oil",
                     "kull", "kol", "olje", "råolje", "petroleum"]

termlist7_2n = ["reduc", "decreas", "improv", "support", "encourag", "intervention", "policy", "policies", "legislation", "incentiv",
                "reduser", "reduksjon", "mink", "bedre", "betr", "støtte", "stønad", "oppmuntr", "oppmod", "intervensjon", "inngrip", "politikk", "retningslin", "lovgiv", "insentiv"]

termlist7_2o = ["reliance", "consumption", "transition", "substitut", "primary source",
                "avhengig", "forbruk", "overgang", "erstat", "primærkilde"]

termlist7_2ptrunk = ["use", "usage", 
                     "bruk"]

termlist7_2q = ["phase out", "phasing out", "energy transition", "energy strateg", "energy management", "energy planning", "energy policy",
                "energy services", "energy sector", "energy supply", "energy supplies", "energy generation", "global share", "global electricity", "energy mix",
                "coal consumption", "fossil fuel consumption", "consumption of fossil fuel", "primary source",
                
                "utfas", "fase ut", "energistrategi", "energiledelse", "energileiing", "energiplan", "energipolitikk", "energitjeneste", "energiteneste",
                "global andel", "global elektrisitet", "energimiks", "forbruk", "primær kilde", "primær kjelde", "primærkilde", "primærkjelde"]

termlist7_2r = ["fossil fuel", "natural gas", "grey hydrogen", "conventional energy", "petroleum",
                "fossilt brensel", "fossile brensl", "fossilt brennstoff", "fossile brennstoff", "naturgass", "grått hydrogen", "konvensjonell energi"]

termlist7_2NOT = ["palm oil", "oil palm", "olive oil", "coconut oil", "vegetable oil", "eucalyptus oil", "cooking oil", "fish oil", "liver oil",
                  "nutrition", "cholesterol", "obes", "human consum",
                  "cylinder oil", "lubricat", "lube oil", "engine oil"
                 ] #Not an issue in Norwegian as "olje" is normally used as part of another word (e.g. "olivenolje")

phrasedefault7_2m = r'(?:{})'.format('|'.join(termlist7_2m))
phrasespecific7_2mtrunk = r'\b(?:{})\b'.format('|'.join(termlist7_2mtrunk))
phrasedefault7_2n = r'(?:{})'.format('|'.join(termlist7_2n))
phrasedefault7_2o = r'(?:{})'.format('|'.join(termlist7_2o))
phrasespecific7_2ptrunk = r'\b(?:{})\b'.format('|'.join(termlist7_2ptrunk))
phrasedefault7_2q = r'(?:{})'.format('|'.join(termlist7_2q))
phrasedefault7_2r = r'(?:{})'.format('|'.join(termlist7_2r))
phrasedefault7_2NOT = r'(?:{})'.format('|'.join(termlist7_2NOT))
```


```python
#Search 7_2mnop
Data.loc[(
    (
        (
            (
                (Data['result_title'].str.contains(phrasedefault7_2m, na=False, case=False))
                |(Data['result_title'].str.contains(phrasespecific7_2mtrunk, na=False, case=False))
            )
        &
            (
                ((Data['result_title'].str.contains(phrasedefault7_2n, na=False, case=False)) & (Data['result_title'].str.contains(phrasespecific7_2ptrunk, na=False, case=False)))
                | (Data['result_title'].str.contains(phrasedefault7_2o, na=False, case=False))
            )
        )
    |
        (
            (
                (Data['result_title'].str.contains(phrasedefault7_2r, na=False, case=False))
                |(Data['result_title'].str.contains(phrasespecific7_2mtrunk, na=False, case=False))
            )
        & (Data['result_title'].str.contains(phrasedefault7_2q, na=False, case=False))
        )
    )
    & (~Data['result_title'].str.contains(phrasedefault7_2NOT, na=False, case=False))
),"tempsdg07_02"] = "SDG07_02"

print("Number of results = ", len(Data[(Data.tempsdg07_02 == "SDG07_02")]))  
```


```python
test=Data.loc[(Data.tempsdg07_02 == "SDG07_02"), ("result_id", "result_title")]
test.iloc[0:25, ]
```

### SDG 7.3

*By 2030, double the global rate of improvement in energy efficiency*

*Innen 2030 få forbedringen av energieffektivitet på verdensbasis til å gå dobbelt så fort*

#### Phrase 1
This search is simplified compared to the WOS search, to adapt to a title search.


```python
# Term lists
termlist7_3a = ["energy intensity", 
                "energiintensitet" ]

# As "energy intensity" is such a specialized term, we found it sufficient to search for it alone in the title search.

phrasedefault7_3a = r'(?:{})'.format('|'.join(termlist7_3a))
```


```python
## Search 7_3a 
Data.loc[(
 (Data['result_title'].str.contains(phrasedefault7_3a, na=False, case=False))
),"tempsdg07_03"] = "SDG07_03"

print("Number of results = ", len(Data[(Data.tempsdg07_03 == "SDG07_03")]))  
```


```python
test=Data.loc[(Data.tempsdg07_03 == "SDG07_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2
This search is simplified compared to the WOS search, to adapt to a title search.


```python
# Term lists
termlist7_3e = ["energy consum", 
                "energiforbruk"]

#termlist7_3f = ["decoupl", "de coupl", 
#                "kobl", "kopl"]

termlist7_3g = ["econom", "GDP", 
                "økonomi", "BNP"]

#In this phrase, searching with the same phrases and limitations as in Web of Science was quite restrictive. 
#We therefore chose to simplify the search and accept a combination of "energy consum" and "econom" or "GDP" in the title as sufficient to be included (without "decoupling")

phrasedefault7_3e = r'(?:{})'.format('|'.join(termlist7_3e))
#phrasedefault7_3f = r'(?:{})'.format('|'.join(termlist7_3f))
phrasedefault7_3g = r'(?:{})'.format('|'.join(termlist7_3g))
```


```python
## Search 7_3eg 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault7_3e, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault7_3g, na=False, case=False))
),"tempsdg07_03"] = "SDG07_03"

print("Number of results = ", len(Data[(Data.tempsdg07_03 == "SDG07_03")]))  
```


```python
test=Data.loc[(Data.tempsdg07_03 == "SDG07_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
# Term lists

# A direct translation of the Web of Science search into Norwegian language gave barely any results. 
# We therefore allowed a few terms for energy efficiency and energy saving in Norwegian to stand alone in order to capture some more relevant titles (list 3no below). 
# This was not done in english because it is poor precision.
termlist7_3h = ["energy efficien", "energy utilisation efficiency", "energy utilization efficiency", "energy saving", "energy loss", "energy conservation",
                "energieffektiv", "effektiv energibruk", "energisparing", "energiøkonomisering", "energitap", "energirasjonering", "strømrasjonering"]

termlist7_3i = ["housing", "houses", "homes", "household", "domestic", "residential", "building", "cities", "service sector", "office", "retail", "food services", "restaurant", 
                "hotel", "warehouses", "lighting", "lamps", "cooking", "appliances", "white goods", "plug-in device", "smart", "space cooler", "air condition", "space heat", 
                "room heating", "district heating", "heat pump", "HVAC", "industry", "industrial", "manufacturing", "technolog", "transport", 
                "vehicles", "cars", "train", "airplane", "aeroplane", "ship", "freight", 
                "telecomm", "data centre", "data center", "data network", "server", "wireless",

                "hus", "hjem", "heim", "hushold", "hushald", "bolig", "bustad", "bygning", "by", "tjenesteytende næring", "tjenesteytande næring", "tertiærnæring", 
                "kontor", "salg", "detaljhandel", "varehus", "kjøpesent", "lys", "ljos", "belysning", "lampe", "matlaging", "apparat", "maskin", "hvitevare", 
                "smart", "kjøler", "klimaanlegg", "oppvarm", "varmepumpe", "VVS", "industri", "produksjon", "teknologi",
                "kjøretøy", "køyretøy", "biler", "bilar", "tog", "fly", "skip", "frakt", "last", "telekomm", "datasent", "datanett", "trådløs"]

termlist7_3j = ["energy efficien", "energy conservation", 
                "energieffektiv", "energirasjonering", "strømrasjonering", "energisparing", "energiøkonomiser", "enøk"]

termlist7_3k = ["policy", "policies", "framework", "legislation", "management", "plan", "initiativ", "intervention", "incentive", "invest"
                "politikk", "retningslin", "rammeverk", "lovgiv", "ledelse", "leiing", "intervensjon", "inngripen", "insentiv"]  

termlist7_3l = ["energy efficien",
                "energieffektiv"]

termlist7_3m = ["green bond", "climate bond", "energy certificat", "green certificat", "energy sustainability", "minimum energy performance", "energy labelling", "energy standard", 
                "energy efficiency standard", "sustainable development", 
                
                "grønne obligasjon", "grøne obligasjon", "klimaobligasjon", "energisertifi", "grøn sertifi", "grønt sertifi", "grønne sertifi", "energimerk", 
                "energistandard", "energieffektivitetsstandard", "bærekraftig utvikling", "berekraftig utvikling"] 

termlist7_3standalone = ["energy efficien", "energy utilisation efficiency", "energy utilization efficiency", "energy saving", "energy conservation",
                         "energieffektiv", "effektiv energibruk", "energispar", "energiøkonomiser", "energirasjonering", "strømrasjonering"]

phrasedefault7_3h = r'(?:{})'.format('|'.join(termlist7_3h))
phrasedefault7_3i = r'(?:{})'.format('|'.join(termlist7_3i))
phrasedefault7_3j = r'(?:{})'.format('|'.join(termlist7_3j))  
phrasedefault7_3k = r'(?:{})'.format('|'.join(termlist7_3k))
phrasedefault7_3l = r'(?:{})'.format('|'.join(termlist7_3l))
phrasedefault7_3m = r'(?:{})'.format('|'.join(termlist7_3m))              
phrasedefault7_3standalone = r'(?:{})'.format('|'.join(termlist7_3standalone))
```


```python
## Search 7_3hijklmno 

#Title and abstract search
#Data.loc[(
#    ((Data['result_title'].str.contains(phrasedefault7_3h, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_3i, na=False, case=False)))
#    |((Data['result_title'].str.contains(phrasedefault7_3j, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_3k, na=False, case=False)))
#    |((Data['result_title'].str.contains(phrasedefault7_3l, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_3m, na=False, case=False)))
#),"tempsdg07_03"] = "SDG07_03"

#Title search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault7_3standalone, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault7_3h, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_3i, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasedefault7_3j, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_3k, na=False, case=False)))
),"tempsdg07_03"] = "SDG07_03"

print("Number of results = ", len(Data[(Data.tempsdg07_03 == "SDG07_03")])) 
```


```python
test=Data.loc[(Data.tempsdg07_03 == "SDG07_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4
We have simplified the search as we are only searching titles, and left out specific energy terms. All that is required now is terms for "energy efficien" combined with "sufficien", or the title to contain "energy suffici*".


```python
# Term lists
termlist7_3n = ["energy suffici"]

termlist7_3q = ["sufficien", "suffisien", 
                "tilstrekkelig"]

termlist7_3r = ["energy efficien", 
                "energieffektiv"]

phrasedefault7_3n = r'(?:{})'.format('|'.join(termlist7_3n))
phrasedefault7_3q = r'(?:{})'.format('|'.join(termlist7_3q))
phrasedefault7_3r = r'(?:{})'.format('|'.join(termlist7_3r))
```


```python
## Search 7_3nqr 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault7_3n, na=False, case=False))
    |
    (
        (Data['result_title'].str.contains(phrasedefault7_3q, na=False, case=False)) 
        &(Data['result_title'].str.contains(phrasedefault7_3r, na=False, case=False))  
    )
),"tempsdg07_03"] = "SDG07_03"

print("Number of results = ", len(Data[(Data.tempsdg07_03 == "SDG07_03")])) 
```


```python
test=Data.loc[(Data.tempsdg07_03 == "SDG07_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 7.a

*By 2030, enhance international cooperation to facilitate access to clean energy research and technology, including renewable energy, energy efficiency and advanced and cleaner fossil-fuel technology, and promote investment in energy infrastructure and clean energy technology*

*Innen 2030 styrke det internasjonale samarbeidet for å lette tilgangen til forskning og teknologi på området ren energi, inkludert fornybar energi, energieffektivisering og avansert og renere teknologi for fossilt brensel, og fremme investeringer i energiinfrastruktur og teknologi for ren energi*

#### Phrase 1


```python
# Term lists
termlist7_a1 = ["development spending", "cooperation fund", 
                "bistand", "utviklingshjelp", "u-hjelp", "samarbeidsfond"]
termlist7_a1caps = ["ODA"]
termlist7_a2 = ["international", "development", "foreign",
                "internasjonal", "utvikling", "utland", "utenlandsk", "utanlands", "utalands"]
termlist7_a3 = ["cooperat", "co-operat", "collaborat", "network", "partnership", "aid", "assistance", "fund", "grant", "financing", "financial resources", "capital flow",
                "samarbeid", "felles", "nettverk", "partner", "hjelp", "bistand", "støtte", "stønad", "finans", "økonomi", "ressurs", "kapital"]
termlist7_a4 = ["knowledge", "technolog", "technical", "research", "scientific", "R&D",
                "kunnskap", "teknolog", "teknisk", "forskning", "forsking", "vitenskapelig", "vitskapeleg", "FOU"]
termlist7_a5 = ["access", "capacity", "transfer", "sharing", "share", "cooperat", "co-operat", "collaborat", "partnership",
                "tilgang", "kapasitet", "overfør", "deling", "dele", "samarbeid", "koopera", "partner"]
termlist7_a6 = ["invest", "financing", "funding", "financial resources", "economic support", "economic assistance", "green bond", "climate bond",
                "finans", "økonomi", "støtte", "stønad", "grønne obligasjon", "grøne obligasjon", "klimaobligasjon"]
termlist7_a7 = ["financial", "monetary",
                "finansiell", "monetær", "penge"]
termlist7_a8 = ["support", "assist",
                "støtte", "stønad"]

termlist7_a9 = ["energy research", "energy efficiency research", "energy transition", "energy technolog",
                "energiforskning", "energiforsking", "energiomstilling", "energiteknologi"]

termlist7_a10 = ["technolog", "innovation", "R&D",
                 "teknologi", "innovasjon", "FOU"]

termlist7_a11 = ["clean energy", "green energy", "decarboni", "low carbon", "energy efficien", "renewable", "solar", 
                 "wind", "geothermal", "hydroelectric", "hydro electric", "hydro power", "marine energy", "tidal energy", "wave energy",
                 
                 "ren energi", "grønn energi", "avkarboniser", "lavkarbon", "lågkarbon", "energieffektiv", "fornybar", "solcelle", "solkraft", "solenergi", "solcelle", "solkraft", "solenergi", 
                 "vind", "geotermisk", "hydroelektrisk", "vannkraft", "vasskraft", "havenergi", "tidevannsenergi", "tidvass", "bølgeenergi"]    

phrasedefault7_a1 = r'(?:{})'.format('|'.join(termlist7_a1))
phrasespecific7_a1caps = r'\b(?:{})\b'.format('|'.join(termlist7_a1caps))
phrasedefault7_a2 = r'(?:{})'.format('|'.join(termlist7_a2))
phrasedefault7_a3 = r'(?:{})'.format('|'.join(termlist7_a3))
phrasedefault7_a4 = r'(?:{})'.format('|'.join(termlist7_a4))
phrasedefault7_a5 = r'(?:{})'.format('|'.join(termlist7_a5))
phrasedefault7_a6 = r'(?:{})'.format('|'.join(termlist7_a6)) 
phrasedefault7_a7 = r'(?:{})'.format('|'.join(termlist7_a7))
phrasedefault7_a8 = r'(?:{})'.format('|'.join(termlist7_a8))
phrasedefault7_a9 = r'(?:{})'.format('|'.join(termlist7_a9))
phrasedefault7_a10 = r'(?:{})'.format('|'.join(termlist7_a10))
phrasedefault7_a11 = r'(?:{})'.format('|'.join(termlist7_a11))                                                                                        
```


```python
## Search 7_a1234567891011
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault7_a1, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific7_a1caps, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_a2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a3, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault7_a4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a5, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault7_a6, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_a7, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a8, na=False, case=False)))
    )
    &
    (
        (Data['result_title'].str.contains(phrasedefault7_a9, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_a10, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a11, na=False, case=False)))
    ) 
),"tempsdg07_a"] = "SDG07_0a"

print("Number of results = ", len(Data[(Data.tempsdg07_a == "SDG07_0a")]))  
```


```python
test=Data.loc[(Data.tempsdg07_a == "SDG07_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
# Term lists
termlist7_a12 = ["development spending", "cooperation fund", 
                 "offisiell utviklingsbistand", "offentlig utviklingsbistand", "bistand", "utviklingshjelp", "u-hjelp", "samarbeidsfond"]
termlist7_a1caps = ["ODA"]
termlist7_a13 = ["international", "development", "foreign", 
                 "internasjonal", "utvikling", "utland", "utaland", "utanland", "utenlandsk"]
termlist7_a14 = ["cooperat", "co-operat", "collaborat", "network", "partnership", "aid", "assistance", "fund", "grant", "financing", 
                 "financial resources", "capital flow",
                 "samarbeid", "felles", "nettverk", "partnerskap", "hjelp", "bistand", "støtte", "stønad", "finansier", "økonomisk ressurs", 
                 "økonomiske ressurs", "finansiell ressurs", "finansielle ressurs", "kapitalflyt", "kapitalstr"]
termlist7_a15 = ["invest", "financing", "funding", "financial resources", "economic support", "economic assistance", "green bond", "climate bond",
                "finansier", "finansiell ressurs", "finansielle ressurs", "økonomisk støtte", "økonomisk stønad", "grønne obligasjon", "grøne obligasjon", "klimaobligasjon"]        
termlist7_a16 = ["financial", "monetary", 
                 "finansiell", "monetær", "penge"] 
termlist7_a17 = ["support", "assist", 
                 "støtte", "stønad", "assistanse"] 

termlist7_a18 = ["clean energy", "energy service", "energy sector", "electrical infrastructure", "electricity supply", "power supply", "community energy", 
                 "community renewable energy", "electrical grid", "power grid", "grid extension", "microgrid", "micro grid", "micro-grid", 
                 "minigrid", "mini grid", "mini-grid", "smartgrid", "smart grid", "smart-grid", "energy storage system", "energy transition",
                 
                 "ren energi", "rein energi", "energitjeneste", "energiteneste", "energisektor", "energiinfrastruktur", "elektrisk infrastruktur", "energiforsyning",
                 "strømforsyning", "straumforsyning", "kraftforsyning", "små kraftverk", "minikraftverk", "mikrokraftverk", 
                 "energisamfunn", "mikronett", "øydrift", "smartnett", "energilagring", "energiomstilling"]
termlist7_a19 = ["energy", "electricity",
                 "energi", "elektrisitet", "strøm", "straum", "kraft"]
termlist7_a20 = ["infrastructure", "technology", "off grid", "offgrid", "off-grid", "decentralised", "decentralized", "cooperative",
                 "infrastruktur", "teknologi", "mikronett", "desentral", "kooperativ"]
termlist7_a21 = ["power station", "power generation", "energy generation", "generator",
                 "kraftstasjon", "kraftverk", "kraftproduksjon", "strømproduksjon", "straumproduksjon"]
termlist7_a22 = ["modern", "clean", "sustainable", "renewable", "solar", "wind", "geothermal", "hydroelectric", "hydro electric", "hydropower", 
                 "marine", "tidal", "wave energy",
                 "rein", "bærekraftig", "berekraftig", "fornybar", "sol", "vind", "geotermisk", "hydroelektrisk", "vannkraft", "vasskraft", 
                 "hav", "tidevann", "tidvass", "bølgeenergi"]                                        

phrasedefault7_a12 = r'(?:{})'.format('|'.join(termlist7_a12))
phrasespecific7_a1caps = r'\b(?:{})\b'.format('|'.join(termlist7_a1caps))
phrasedefault7_a13 = r'(?:{})'.format('|'.join(termlist7_a13))
phrasedefault7_a14 = r'(?:{})'.format('|'.join(termlist7_a14))
phrasedefault7_a15 = r'(?:{})'.format('|'.join(termlist7_a15))
phrasedefault7_a16 = r'(?:{})'.format('|'.join(termlist7_a16))
phrasedefault7_a17 = r'(?:{})'.format('|'.join(termlist7_a17))
phrasedefault7_a18 = r'(?:{})'.format('|'.join(termlist7_a18))
phrasedefault7_a19 = r'(?:{})'.format('|'.join(termlist7_a19))
phrasedefault7_a20 = r'(?:{})'.format('|'.join(termlist7_a20))
phrasedefault7_a21 = r'(?:{})'.format('|'.join(termlist7_a21))
phrasedefault7_a22 = r'(?:{})'.format('|'.join(termlist7_a22))
```


```python
## Search 7_a1213141516171819202122
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault7_a12, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific7_a1caps, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_a13, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a14, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault7_a15, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_a16, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a17, na=False, case=False)))  
    ) 
    &
    (
        (Data['result_title'].str.contains(phrasedefault7_a18, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault7_a19, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a20, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault7_a21, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_a22, na=False, case=False)) )
    )
),"tempsdg07_a"] = "SDG07_0a"

print("Number of results = ", len(Data[(Data.tempsdg07_a == "SDG07_0a")]))
```


```python
test=Data.loc[(Data.tempsdg07_a == "SDG07_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 7.b

*By 2030, expand infrastructure and upgrade technology for supplying modern and sustainable energy services for all in developing countries, in particular least developed countries, small island developing States and landlocked developing countries, in accordance with their respective programmes of support*

*Innen 2030 bygge ut infrastruktur og oppgradere teknologi for å tilby moderne og bærekraftige energitjenester til alle innbyggere i utviklingsland, særlig i de minst utviklede landene, små utviklingsøystater og kystløse utviklingsland, i samsvar med landenes respektive støtteprogram*


```python
# Term lists
termlist7_b1 = ["energy service", "energy sector", "electrical infrastructure", 
                "electricity supply", "power supply", "energy", "electricity",
                
                "energitjeneste", "energiteneste", "energisektor", "elektrisk infrastruktur", "energiinfrastruktur", "elektrisitetsforsyning", 
                "strømforsyning", "straumforsyning", "kraftforsyning", "energi", "elektrisitet"]

termlist7_b2 = ["infrastructure", "technolog", "off grid", "offgrid", "off-grid", "decentralised", "decentralized", "community", "cooperative", "co-operative",
                "electrical grid", "power grid", "grid extension", 
                "microgrid", "micro-grid", "micro grid", "minigrid", "mini-grid", "mini grid", "smartgrid", "smart grid", "smart-grid", "energy storage system",
                
                "infrastruktur", "teknologi", "mikronett", "desentral", "samfunn", "kooperativ", "strømnett", "straumnett", "kraftnett", "elnett", "små kraftverk", "minikraftverk",
                "mikrokraftverk", "øydrift", "smartnett", "energilagring"]

termlist7_b3 = ["power station", "power generation", "energy generation", "generator",
                "kraftstasjon", "kraftverk", "kraftprod", "strømprod", "straumprod"]

termlist7_b4 = ["modern", "clean", "sustainable", "renewable", "decarboni", "low carbon", "solar", "wind", "geothermal", 
                "hydroelectric", "hydro electric", "hydropower", "marine", "tidal", "wave energy",
                
                "moderne", "bærekraftig", "berekraftig", "fornybar", "dekarboniser", "lavkarbon", "lågkarbon", "sol", "vind", "geotermisk", 
                "hydroelektrisk", "vannkraft", "vasskraft", "hav", "tidevann", "tidvass", "bølgeenergi"]                 

phrasedefault7_b1 = r'(?:{})'.format('|'.join(termlist7_b1))
phrasedefault7_b2 = r'(?:{})'.format('|'.join(termlist7_b2))
phrasedefault7_b3 = r'(?:{})'.format('|'.join(termlist7_b3))
phrasedefault7_b4 = r'(?:{})'.format('|'.join(termlist7_b4))        

```


```python
#Search 1 - in SIDS and LDCs data
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault7_b1, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_b2, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault7_b3, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_b4, na=False, case=False)))
    ) 
    & (Data['LMICs']==True)
),"tempsdg07_b"] = "SDG07_b"

print("Number of results = ", len(Data[(Data.tempsdg07_b == "SDG07_b")])) 
```


```python
test=Data.loc[(Data.tempsdg07_b == "SDG07_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 7 mentions



```python
# Term lists
termlist7_1 = ["SDG 7", "SDGs 7", "SDG7", "sustainable development goal 7", 
               "bærekraftsmål 7", "berekraftsmål 7"]
termlist7_2 = ["sustainable development goal", 
               "bærekraftsmål", "berekraftsmål"]
termlist7_3 = ["goal 7", 
               "mål 7"]
termlist7_4 = ["sustainable development goal", "SDG", "goal 7", 
               "bærekraftsmål", "berekraftsmål", "mål 7"]
termlist7_5 = ["energy", 
               "energi"]
termlist7_6 = ["affordable and clean energy", 
               "ren energi til alle", "rein energi til alle"]

phrasedefault7_1 = r'(?:{})'.format('|'.join(termlist7_1))
phrasedefault7_2 = r'(?:{})'.format('|'.join(termlist7_2))
phrasedefault7_3 = r'(?:{})'.format('|'.join(termlist7_3))
phrasedefault7_4 = r'(?:{})'.format('|'.join(termlist7_4))
phrasedefault7_5 = r'(?:{})'.format('|'.join(termlist7_5))   
phrasedefault7_6 = r'(?:{})'.format('|'.join(termlist7_6))

```


```python
## Search 7_123456
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault7_1, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault7_2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_3, na=False, case=False))) 
    |((Data['result_title'].str.contains(phrasedefault7_4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_5, na=False, case=False)))
    |(Data['result_title'].str.contains(phrasedefault7_6, na=False, case=False))
),"tempmentionsdg07"] = "SDG07"

print("Number of results = ", len(Data[(Data.tempmentionsdg07 == "SDG07")]))
```


```python
test=Data.loc[(Data.tempmentionsdg07 == "SDG07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 11

General note: For the Norwegian adaptation, we include some of the major cities by name as synonymyms for "city". 

### SDG 11.1

*By 2030, ensure access for all to adequate, safe and affordable housing and basic services and upgrade slums*

*Innen 2030 sikre at alle har tilgang til tilfredsstillende og trygge boliger og grunnleggende tjenester til en overkommelig pris, og bedre forholdene i slumområder*

#### Phrase 1


```python
#Termlists
termlist11_1a = ["access", "obstacle", "barrier", "hinder", "hindrance", "equitab", "non-equit", "legislat", "govern", "strateg", "policy", "policies" , "framework" , "program",
                 "tilgang", "hindr", "rettferdig", "lovgiv", "lovgje" "politikk", "politisk", "reguler", "rettningslin", "strateg"]

termlist11_1b = ["adequa", "inadequa", "afford", "low cost", "low-cost", "inexpensive", "unsafe", "safety", "secure", "security", "tenure",
                 "adekvat", "tilstrekkel", "høveleg", "dekkende", "dekkande", "billig", "billeg", "rimelig", "rimeleg", "trygg", "sikker"]

termlist11_1c = ["housing", "settlements", "living conditions",
                 "bolig", "bustad", "bosetting", "busetjing", "boforhold"]

phrasedefault11_1a = r'(?:{})'.format('|'.join(termlist11_1a))
phrasedefault11_1b = r'(?:{})'.format('|'.join(termlist11_1b))
phrasedefault11_1c = r'(?:{})'.format('|'.join(termlist11_1c))
```


```python
#Search
Data.loc[(
        (Data['result_title'].str.contains(phrasedefault11_1a, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault11_1b, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault11_1c, na=False, case=False))             
),"tempsdg11_01"] = "SDG11_01"

print("Number of results = ", len(Data[(Data.tempsdg11_01 == "SDG11_01")])) 
```


```python
test=Data.loc[(Data.tempsdg11_01 == "SDG11_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist11_1d = ["access", "obstacle", "barrier", "hinder", "hindrance", "equitab", "non-equit", "legislat", "governan", "strateg", "policy", "policies", "framework", "program",
                 "tilgang", "hinder", "hindr", "rettferdig", "urettferdig", "lovgiv", "lovgje" "politikk", "politisk", "reguler", "strateg"]

termlist11_1e = ["basic service", "basic facilities", "essential service",
                "drinking water", "sanitation", "basic hygiene", "hygiene service", "toilet", "handwashing", "sewage", "WASH facilities", 
                "clean water",
                "waste collection", "waste service", "waste facilit", "garbage service", "garbage collection", 
                "health service", "health facilit", "basic health", "essential health", "healthcare", "health care", "medical care", "essential medical",
                "school service", "school facilit", "basic school", "primary school", "basic education", "education service", "primary education",
                "basic communication service", "basic telecommunication service", "basic information service", "basic information infrastructure",
                "electricity", "energy service", "modern energy", "clean fuel", "clean energy", "modern energy",
                "public open space", "public space", "public green space",
                "basic mobility", "urban mobility", "rural mobility", "all-season road", "transport service", "public transport",

                "grunnleggende tjeneste", "grunnleggjande teneste", "greunnleggende fasilitet", 
                "drikkevann", "drikkevatn", "grunnleggende hygiene", "grunnleggjande hygiene", "kloakk", "toalett", "vannklosett", "vassklosett", "håndvask", "handvask", "sanitær",
                "rent vann", "reint vatn", "reint vann", "innlagt vann", "innlagt vatn", "vanntilgang", "vannforsyning",
                "avfallstjeneste", "avfallsteneste", "søppeltømming", "avfallsinnsamling", "bosteneste", "bosinnsamling", "bostømming", "renovasjon",
                "helsetjeneste", "helseteneste", "fastlege","helsevesen",
                "ungdomsskole", "ungdomsskule", "barneskole", "barneskule", "grunnleggende utdannin", "grunnleggjande utdannin", 
                "kommunikasjonstjenester", "kommunikasjonstenester", "kommunikasjonsinfrastruktur", "grunnleggende kommunikasjon",
                "energitjeneste", "energiteneste", "energilever", "elektrisitet", "energiforsyning", "kraftforsyning", "moderne energi",
                "offentlig rom", "offentlige rom", "offentlege rom", "offentlege rom", "grønt areal", "grønne areal", "grøntområde", "friområde", "friareal", "rekreasjonsområde",
                "offentlig transport", "offentlige transport", "offentleg transport", "offentlege transport", "kollektivtransport", "kollevktivtilb", "transport ordning", 
                "mobilitet"
                ]
                #"xxxxskole"(NO) is specified here to avoid in Norwegian university names, e.g. "Høyskole"

termlist11_1r = ["housing", "settlements", "living conditions",
                 "cities", "megacit", "urban", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "local community", "neighborhood", "neighbourhood", 

                 "bolig", "bustad", "bosetting", "busetjing", "boforhold"
                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "landsby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
                 "samfunn", "lokalsamfunn", "nabolag", 
                 "oslo", "bergen", "trondheim", "stavanger", "tromsø",
                 ]

termlist11_1rtrunc = ["city"] #"city" is prevented truncation due to "capacity" etc.

phrasedefault11_1d = r'(?:{})'.format('|'.join(termlist11_1d))
phrasedefault11_1e = r'(?:{})'.format('|'.join(termlist11_1e))
phrasedefault11_1r = r'(?:{})'.format('|'.join(termlist11_1r))
phrasespec11_1r_trunc = r'\b(?:{})\b'.format('|'.join(termlist11_1rtrunc))
```


```python
#Search
Data.loc[(
       (Data['result_title'].str.contains(phrasedefault11_1d, na=False, case=False))
       & (Data['result_title'].str.contains(phrasedefault11_1e, na=False, case=False))
       & ((Data['result_title'].str.contains(phrasedefault11_1r, na=False, case=False))|(Data['result_title'].str.contains(phrasespec11_1r_trunc, na=False, case=False)))
),"tempsdg11_01"] = "SDG11_01"

print("Number of results = ", len(Data[(Data.tempsdg11_01 == "SDG11_01")])) 
```


```python
test=Data.loc[(Data.tempsdg11_01 == "SDG11_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist11_1s = ["shanty town", "informal settlement",
                 "uformell bosetning", "uformelle bosetning", "uformell busetn", "uformelle busetn"]

termlist11_1strunk = ["slum", "slums"]

phrasedefault11_1s = r'(?:{})'.format('|'.join(termlist11_1s))
phrasedefault11_1strunk = r'\b(?:{})\b'.format('|'.join(termlist11_1strunk))
#truncating "slum" adds noise
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault11_1s, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault11_1strunk, na=False, case=False))             
),"tempsdg11_01"] = "SDG11_01"

print("Number of results = ", len(Data[(Data.tempsdg11_01 == "SDG11_01")])) 
```


```python
test=Data.loc[(Data.tempsdg11_01 == "SDG11_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.2
*By 2030, provide access to safe, affordable, accessible and sustainable transport systems for all, improving road safety, notably by expanding public transport*

*Innen 2030 sørge for at alle har tilgang til trygge, tilgjengelige og bærekraftige transportsystemer til en overkommelig pris og bedre sikkerheten på veiene*

#### Phrase 1 & 2

These two phrases are merged in this search. In addition we changed the structure - now, only terms that are ambiguous are combined with the "city" terms (e.g. "transport", "vehice", "driver")



```python
#Term lists

termlist11_2a = ["safe", "secure", "hazardous","sustainab", "unsafe", "dangerous","accident","access", "availab", "reliab", "afford", "low cost", "low-cost", "expensive", "cost-effective", 
                 "sikker", "trygg", "farlig", "farleg", "risiko", "bærekraftig", "berekraftig", "tilgjengelig", "pålitelig", "rimelig", "billig", "kostbar", "kostnadseffektiv"]
termlist11_2a_trunc = ["risk", "risks", "risky"] 

termlist11_2b = ["transport infrastructure", "public transport", "urban mobilit", "traffic", "roadway", "street", "roundabout",
                 "highway", "motorway", "cycling lane", "cyclist", "cycle path", "bicycle lane", "walkway", "walking path", "sidewalk", "pavement","pedestrian","taxi", "ferry",
                 "the underground", "railway", "airport", 
                 "travel", "car safety", "driver safety", "safe driving", "motorcycle", "automobile", "speed limit",

                 "transportnettverk", "offentlig transport", "offentleg transport", "kollektivtransport", "transportinfrastruktur", "transportsystem", "trafikk", "rundkjøring","rundkøyring", 
                 "motorvei", "motorveg", "sykkelsti", "sykkelve", "syklist", "gangve", "fortau", "drosje", "ferge", "hurtigbåt",
                 "t-bane", "bybane", "jernbane", "flyplass", "kortbane", 
                 "sikkerhet i bil", "motorsykkel", "sjåfør", "kjøring", "kjøyring", "fartsgrense"
                 ] 
                 #"driving" and "driver" combined as otherwise problematic

termlist11_2b2 = ["transport system","transport network", "driver", "vehicl",
                  "reise"]
                  #terms that need to be combined with city-terms, as they are used in e.g. biomedicine
                  #"reise" (NO) is moved here because often used in "reiseliv" (tourism)

termlist11_2c = ["road", "roads", "car", "cars", "bus", "train", "tube", "journey",
                 "veier", "veger", "vegar", "gate", "gater", "buss", "train", "tube", "metro", "tog", "fører", "førere"
                 #"veg", "vei"
                 ]
                #terms where truncation is prevented
                #"vei" and "veg", although relevant terms (= way, road) seem to be used nearly always metaphorically ("way to safer workplaces") so suggest removal for practical reasons

termlist11_2d = ["cities", "megacit", "urban", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "community", "neighborhood", "neighbourhood", 

                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "landsby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
                 "samfunn", "lokalsamfunn", "nabolag", 
                 "oslo", "bergen", "trondheim", "stavanger", "tromsø",
                 ]

termlist11_2dtrunc = ["city"] #"city" is here due to capaCITY etc.

phrasedefault11_2a = r'(?:{})'.format('|'.join(termlist11_2a))
phrasespecific11_2atrunc = r'\b(?:{})\b'.format('|'.join(termlist11_2a_trunc))
phrasedefault11_2b = r'(?:{})'.format('|'.join(termlist11_2b))
phrasedefault11_2b2 = r'(?:{})'.format('|'.join(termlist11_2b2))
phrasespecific11_2c = r'\b(?:{})\b'.format('|'.join(termlist11_2c))
phrasedefault11_2d = r'(?:{})'.format('|'.join(termlist11_2d))

```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault11_2a, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific11_2atrunc, na=False, case=False))
    )
    &
    (
        (Data['result_title'].str.contains(phrasedefault11_2b, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific11_2c, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault11_2b2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_2d, na=False, case=False)))
    )
),"tempsdg11_02"] = "SDG11_02"

print("Number of results = ", len(Data[(Data.tempsdg11_02 == "SDG11_02")]))
```


```python
test=Data.loc[(Data.tempsdg11_02 == "SDG11_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Term lists
termlist11_2e  = ["provide", "provision", "improv", "moderni", "reduc", "increas", "expand", "build", "boost", "rais", "extend", "implement", "establish", "develop", "strengthen", "enhanc",
                 "tilbyr", "etablere", "forbedr", "styrk", "bedring", "betring", "reduser", "bygg", "utvikl", "oppgrad", "muliggjør"]  

termlist11_2f  = ["public transport",
                 "offentlig transport", "offentleg transport", "kollektivtransport"] 

phrasedefault11_2e = r'(?:{})'.format('|'.join(termlist11_2e))
phrasedefault11_2f = r'(?:{})'.format('|'.join(termlist11_2f))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault11_2e, na=False, case=False))
        &(Data['result_title'].str.contains(phrasedefault11_2f, na=False, case=False))
    )
),"tempsdg11_02"] = "SDG11_02"

print("Number of results = ", len(Data[(Data.tempsdg11_02 == "SDG11_02")]))
```


```python
test=Data.loc[(Data.tempsdg11_02 == "SDG11_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.3

*By 2030, enhance inclusive and sustainable urbanization and capacity for participatory, integrated and sustainable human settlement planning and management in all countries*

*Innen 2030 styrke inkluderende og bærekraftig urbanisering og muligheten for en deltakende, integrert og bærekraftig samfunnsplanlegging og forvaltning i alle land*

#### Phrase 1


```python
#Termlists
termlist11_3a = ["sustainab", "inclusiv", "participatory", "participation",
                 "bærekraft", "berekraft", "inkluder", "deltak", "deltag"]

termlist11_3b = ["urbanisation", "urbanization", "urban development", "human settlement planning", "urban planning",
                 "urbanisering", "urban utvikling", "byutvikling", "byplan"]

phrasedefault11_3a = r'(?:{})'.format('|'.join(termlist11_3a))
phrasedefault11_3b = r'(?:{})'.format('|'.join(termlist11_3b))
```


```python
#Search 11_3
phrase11_3ab = Data.loc[(
    (Data['result_title'].str.contains(phrasedefault11_3a, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault11_3b, na=False, case=False))             
),"tempsdg11_03"] = "SDG11_03"

print("Number of results = ", len(Data[(Data.tempsdg11_03 == "SDG11_03")]))  
```


```python
test=Data.loc[(Data.tempsdg11_03 == "SDG11_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist11_3c = ["settlement", 
                 "cities", "megacit", "urban", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "neighborhood", "neighbourhood", 
                 "local communit", 

                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
                 "bosetting", "busetting", 
                 "nabolag", 
                 "lokal samfunn",
                 "oslo", "bergen", "trondheim", "stavanger", "tromsø",
                 ]
termlist11_3c_trunc = ["city"]

termlist11_3d = ["manag",
                 "planleg", "lede", "leiing", "styring", "forvalt"]

termlist11_3d_trunc = ["plan","plans","planning"]  

termlist11_3e = ["democra", "taking part", "sustainab", "participatory", "participation", "stakeholder",
                 "demokrat", "delta", "bærekraft", "berekraft", "interessent"]

phrasedefault11_3c = r'(?:{})'.format('|'.join(termlist11_3c))
phrasedefault11_3c_trunc = r'\b(?:{})\b'.format('|'.join(termlist11_3c_trunc))
phrasedefault11_3d = r'(?:{})'.format('|'.join(termlist11_3d))
phrasedefault11_3d_trunc = r'\b(?:{})\b'.format('|'.join(termlist11_3d_trunc))
phrasedefault11_3e = r'(?:{})'.format('|'.join(termlist11_3e))
```


```python
#Search 11_3
phrase11_3cde = Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault11_3c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault11_3c_trunc, na=False, case=False)))
    & ((Data['result_title'].str.contains(phrasedefault11_3d, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault11_3d_trunc, na=False, case=False)))
    & (Data['result_title'].str.contains(phrasedefault11_3e, na=False, case=False))             
),"tempsdg11_03"] = "SDG11_03"

print("Number of results = ", len(Data[(Data.tempsdg11_03 == "SDG11_03")]))  
```

### SDG 11.4

*Strengthen efforts to protect and safeguard the world’s cultural and natural heritage*

*Styrke innsatsen for å verne og sikre verdens kultur- og naturarv*


```python
#Termlists
termlist11_4a = ["manag", "maintain", "conservation", "conserving", "conserve", "preserv", "sustain", "protect", "safeguard",
                 "forvalt", "vedlikeh", "bevar", "konserver", "ta vare på", "oppretthold", "oppretthald", "sikre", "beskytte", "verne", "verna", "vern av", "frede", "freda", "fredning", "freding",
                 ]

termlist11_4b = ["cultural heritage", "culture heritage", "cultural landscape", "heritage object", "heritage building", "heritage site", "museum",
                 "archaeological place", "archaeological site", "historical place", "historical building", "historical monument", "historical artefact",
                 "natural heritage", "nature formation", "geopark", "nature park", "nature reserv", "zoo", "zoological garden", "botanical garden", "aquarium", "aquaria",

                 "kulturarv", "kulturlandskap", "kulturminne", "historisk bygning", "historisk sted",
                 "arkeologisk sted", "arkeologisk stad", "arkelogisk kulturminne", "fornminne", "arkeologisk område", "historisk monument", "historisk gjenstand",
                 "naturarv", "naturformasjon", "naturpark", "nasjonalpark", "naturreservat", "dyrehage", "zoologisk hage", "botanisk hage", "akvarium", "akvarie"
                 ]

phrasedefault11_4a = r'(?:{})'.format('|'.join(termlist11_4a))
phrasedefault11_4b = r'(?:{})'.format('|'.join(termlist11_4b))
```


```python
#Search 11_4
phrase11_4ab = Data.loc[(
                 (Data['result_title'].str.contains(phrasedefault11_4a, na=False, case=False))&
                 (Data['result_title'].str.contains(phrasedefault11_4b, na=False, case=False))           
),"tempsdg11_04"] = "SDG11_04"

print("Number of results = ", len(Data[(Data.tempsdg11_04 == "SDG11_04")]))  
```


```python
test=Data.loc[(Data.tempsdg11_04 == "SDG11_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.5

*By 2030, significantly reduce the number of deaths and the number of people affected and substantially decrease the direct economic losses relative to global gross domestic product caused by disasters, including water-related disasters, with a focus on protecting the poor and people in vulnerable situations*

*Innen 2030 oppnå en betydelig reduksjon i antall dødsfall og antall personer som rammes av katastrofer, inkludert vannrelaterte katastrofer, og i betydelig grad minske de direkte økonomiske tapene i verdens samlede bruttonasjonalprodukt som følge av slike katastrofer, med vekt på å beskytte fattige og personer i utsatte situasjoner*

#### Phrase 1


```python
#Termlists
termlist11_5a = ["disaster", "catastrophe", 
                 "katastrofe", "krise"]
termlist11_5b = ["extreme", 
                 "ekstrem"]
termlist11_5c = ["climat", "weather", "precipitation", "rain", "snow", "temperatur", "storm", "wind",
                 "klima", "vær", "nedbør", "regn", "snø", "vind"]
termlist11_5d = ["natural", "climat","anthropogenic", "environmental", "deforestation", "desertification", "degradation", "pollution", "erosion", "chemical", "heavy metal", "pesticide", "biological", 
                 "zoonotic", "technological", "radioactive", "nuclear", "cyber", "industrial", "construction", "transportation",
                 "naturl", "klima", "antropogen", "miljømessig", "avskoging", "forørkning", "forørking", "forverring", "ødelegging", "øydelegging", "forurensing", "forureining", "erosjon", "avrenning",
                 "kjemisk", "tungmetall", "plantegift", "plantevernmid", "insekticid", "fungicid", "biologisk", "zoonotisk", "teknologisk", "radioaktiv", "atom", "industriell", "bygge",
               ]
termlist11_5e = ["hazard",
                 "fare", "risiko"]  
termlist11_5f = ["extreme climat", "extreme weather", "extreme precipitation", "extreme rain", "extreme snow", "extreme temperatur", "extreme storm", "extreme wind", 
                 "rogue wave", "tsunami", "cyclone", "typhoon", "hurricane", "tornado", 
                 "drought", "flood", 
                 "avalanche", "landslide", "land-slide", "land slide", "rockslide", "rock-slide", "rock slide", "rockfall", "surface collapse", "mudflow", "mud-flow", 
                 "cold spell", "cold wave", "dzud", "blizzard", "snowstorm", 
                 "heatwave", "heat-wave", 
                 "earthquake", "volcan", "ash cloud", "ash fall", "tephra", 
                 "wildfire", "wild-fire", "wild fire", "forest-fire", "forest fire", "forestfire", 
                 "sea-level rise", "sea-level change", "rising sea-level", 
                 "armed conflict", "political instability", "civil instability", "politically volatile", 
                 "unrest", "financial crash", "financial shock", "economic downturn", "economic shock",

                 "ekstremvær", "ekstremver", 
                 "tropisk lavtrykk", "tropisk lågtrykk", "flodbølg", "monsterbølg", "ekstrembølg", 
                 "orkan",  "tyfon", "syklon", "snøstorm", 
                 "flom", "flaum", "oversvøm", "ovefløym", "tørke", 
                 "snøskred", "skred", "snøras", "lavine", "jordskred", "jordras", "sørpeskred", "leirras", "leirskred", "steinras", "steinskred", "synkehull", 
                 "uvanlig kulde", "uvanlig kaldt", "uvanleg kulde", "uvanleg kaldt", "ekstrem kuld", "ekstremkuld", "kuldebølg", "snøstorm", 
                 "varmebølg", "hetebølg", "ekstrem varm", "ekstremvarm", "uvanlig varm", "uvanleg varm", 
                 "jordskjelv", "vulkan", "askenedfall", "oskenedfall", "askesky", "oskesky", 
                 "skogbrann", "gressbrann", "grasbrann", "lyngbrann", 
                 "havnivåstigning", "stormflo", 
                 "politisk ustabilitet", "væpnede konflikter", "væpnet konflikt", "væpna konflikt", "borgerkrig", "borgarkrig", "fremmedkrig", "finanskrise", "finanssjokk", 
                 "finanskatastrofe", "finanskræsj", "økonomisk nedgang", "økonomisk sjokk", "økonomisk katastrofe"
                 ]   
termlist11_5ftrunc = ["war", "wars", 
                      "krig", "ras"]  #terms where we need to prevent truncation             
#termlist11_5g = ["sea level",
#                 "havnivå"] 
#termlist11_5h = ["change", "changing", "rising", "rise",
#                 "endre", "endring", "øke", "auke", "økning", "heve", "heving"] 
termlist11_5j = ["volatil", "unstable", "instability", "unrest",
                 "flyktig", "ustabil", "instabilitet", "uro"]
termlist11_5k = ["political", "civil",
                 "politisk", "sivil"]

termlist11_5l = ["death", "casualt", "survivors", "fatal",
                 "død", "daud" "offer", "ofre", "overlevende", "overlevande"]

termlist11_5s = ["affected", "injur", "trauma", "displaced", "missing",
                 "berørte", "skadde", "traumatisert", "fordrevne", "fordrivne", "savnede", "savnet", "sakna"]
termlist11_5t = ["people", "person", "civilian", "women", "men", "child",
                 "folk", "sivile", "kvinner", "menn", "barn", "born"]

termlist11_5m = ["surviv", "mortalit",
                 "overlev", "død"]

termlist11_5n = ["people", "human", "patient", "victim", "civilian", 
                 "city","cities", "megacit", "urban", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "community", "neighborhood", "neighbourhood", 
                 "public", "poverty", "the poor", "the poorest", "rural poor", "urban poor", "working poor", "destitute", "living in poverty", "the vulnerable", "vulnerable group", 
                 "vulnerable communit", "marginalised group", "marginalized group", "marginalised communit", "marginalised communit", "disadvantaged group", "disadvantaged communit", 
                 "slum", "shanty town", "informal settlement", "homeless", "disabled", "disabilities", "disability", "elderly", "elders", "pensioners", "vulnerable seniors", "unemployed"
                 "women", "woman", "girl", "pregnant", "pregnancy", "maternity", "child", "children", "infant", "babies", "newborn", "toddler", "youth", "sexual minorit", "LGBT", "lesbian", 
                 "gay", "bisexual", "transgender", "living with HIV", "living with AIDS", "ethnic minorit", "minority group", "refugee", "migrant", "asylum", "indigenous group",
                 
                 "folk", "menneske", "pasient", "offer", "sivil", "borger", "borgar", 
                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "landsby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
                 "lokalsamfunn", "nabolag", 
                 "fattig", "lavinntekt", "lav inntekt", "låginntekt", "låg inntekt", "sårbar", "marginalisert", "diskrimin", "uformell bosetting", "uformell busetnad", "uformelle bosettinger", 
                 "uformelle busetnader", "hjemløs","heimlaus", "uføre", "funksjonshem", "eldre", "de gamle", "dei gamle", "pensjonist", "arbeidsløs","arbeidslaus", "kvinne", "jente", "gravid", 
                 "barn", "born", "babier", "nyfødt", "nyfødd", "ungdom", "seksuell minoritet", "seksuelle minoritet", "urfolk", "urinnvånarar", "urbefolkning", "urinnvånere", "sápmi", "sami", 
                 "minoritet", "jøder", "jådar", "kvener", "kvenar", "norskfinn", "skogfinn", "romani", "tatere", "taterar", "asylsøk", "flyktning", "innvandrer", "innvandrar", "transperson", 
                 "lesbisk", "homofile", "bifile", "lbht", "interkjønn", "leve med aids", "leve med hiv", "lever med aids", "lever med hiv"
                 ]     
termlist11_5o = ["poor", "poorest", "low income", "lower income", "lowest income"]  #other terms/norwegian terms already covered in 5n
termlist11_5p = ["household", "people", "children", "communit",
                "husholdning", "hushaldning", "folk", "menneske", "samfunn"]
termlist11_5q = ["person", "people", "adult",
                "folk", "menneske", "voksen", "vaksen"]
termlist11_5r = ["vulnerable", "marginalised", "marginalized", "disadvantaged", "discriminated", "displaced", "patient", "trans", "intersex", "older", "old", "elderly", "retired", "indigenous", 
                "sårbar", "marginalisert", "diskrimin", "fordrev", "pasient", "transperson", "lesbisk", "homofile", "bifile", "lbht", "interkjønn" "uføre", "funksjonshem", "eldre", "de gamle", 
                "dei gamle", "urfolk", "urinnvånarar", "urbefolkning", "urinnvånere"]

phrasedefault11_5a = r'(?:{})'.format('|'.join(termlist11_5a))
phrasedefault11_5b = r'(?:{})'.format('|'.join(termlist11_5b))
phrasedefault11_5c = r'(?:{})'.format('|'.join(termlist11_5c))
phrasedefault11_5d = r'(?:{})'.format('|'.join(termlist11_5d))
phrasedefault11_5e = r'(?:{})'.format('|'.join(termlist11_5e))
phrasedefault11_5f = r'(?:{})'.format('|'.join(termlist11_5f))
phrasedefault11_5ftrunc = r'\b(?:{})\b'.format('|'.join(termlist11_5ftrunc))
#phrasedefault11_5g = r'(?:{})'.format('|'.join(termlist11_5g))
#phrasedefault11_5h = r'(?:{})'.format('|'.join(termlist11_5h))
phrasedefault11_5j = r'(?:{})'.format('|'.join(termlist11_5j))
phrasedefault11_5k = r'(?:{})'.format('|'.join(termlist11_5k))
phrasedefault11_5l = r'(?:{})'.format('|'.join(termlist11_5l))
phrasedefault11_5m = r'(?:{})'.format('|'.join(termlist11_5m))
phrasedefault11_5n = r'(?:{})'.format('|'.join(termlist11_5n))
phrasedefault11_5o = r'(?:{})'.format('|'.join(termlist11_5o))
phrasedefault11_5p = r'(?:{})'.format('|'.join(termlist11_5p))
phrasedefault11_5q = r'(?:{})'.format('|'.join(termlist11_5q))
phrasedefault11_5r = r'(?:{})'.format('|'.join(termlist11_5r))
phrasedefault11_5s = r'(?:{})'.format('|'.join(termlist11_5s))
phrasedefault11_5t = r'(?:{})'.format('|'.join(termlist11_5t))
#The NOT-part at the end of WoS string is not included, as probably not needed/useful in title searching
```


```python
#Search 11_5
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault11_5a, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault11_5b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5c, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault11_5d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5e, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault11_5j, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5k, na=False, case=False)))          
        |(Data['result_title'].str.contains(phrasedefault11_5f, na=False, case=False))
        |(Data['result_title'].str.contains(phrasedefault11_5ftrunc, na=False, case=False))
    )
    &
    (
        (Data['result_title'].str.contains(phrasedefault11_5l, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault11_5s, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5t, na=False, case=False)))
        |(
            (Data['result_title'].str.contains(phrasedefault11_5m, na=False, case=False))
            &
            ( 
                (Data['result_title'].str.contains(phrasedefault11_5n, na=False, case=False))
                |((Data['result_title'].str.contains(phrasedefault11_5o, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5p, na=False, case=False)))
                |((Data['result_title'].str.contains(phrasedefault11_5q, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5r, na=False, case=False)))
            )
        )
    )        
),"tempsdg11_05"] = "SDG11_05"

print("Number of results = ", len(Data[(Data.tempsdg11_05 == "SDG11_05")])) 
```


```python
test=Data.loc[(Data.tempsdg11_05 == "SDG11_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
                 
termlist11_52l = ["domestic product", "gross global produc",
                 "nasjonalprodukt", "bnp"]
termlist11_52ltrunc = ["gdp", "gpp", "ggdp"]
                                          
phrasedefault11_52l = r'(?:{})'.format('|'.join(termlist11_52l))
phrasedefault11_52ltrunc = r'\b(?:{})\b'.format('|'.join(termlist11_52ltrunc))
#acronyms have truncation prevented to avoid results on gdpr
```


```python
#Search 11_5
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault11_5a, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault11_5b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5c, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault11_5d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5e, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault11_5j, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_5k, na=False, case=False)))          
        |(Data['result_title'].str.contains(phrasedefault11_5f, na=False, case=False))
        |(Data['result_title'].str.contains(phrasedefault11_5ftrunc, na=False, case=False))
    )
    &
    (
        (Data['result_title'].str.contains(phrasedefault11_52l, na=False, case=False))
        | (Data['result_title'].str.contains(phrasedefault11_52ltrunc, na=False, case=False))
    )    
),"tempsdg11_05"] = "SDG11_05"

print("Number of results = ", len(Data[(Data.tempsdg11_05 == "SDG11_05")])) 
```


```python
test=Data.loc[(Data.tempsdg11_05 == "SDG11_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.6

*By 2030, reduce the adverse per capita environmental impact of cities, including by paying special attention to air quality and municipal and other waste management*

*Innen 2030 redusere byenes og lokalsamfunnenes negative påvirkning på miljøet (målt per innbygger), med særlig vekt på luftkvalitet og avfallshåndtering i offentlig eller privat regi*

#### Phrase 1


```python
#Term lists

termlist11_6a = ["environmental impact", "impact on the environment", "impacts on the environment","footprint","foot print",
                 "miljøpåvirk","fotavtrykk","påvirke miljø","påverke miljø"]
  
termlist11_6b = ["cities", "megacit", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "local communit", "neighborhood", "neighbourhood", 

                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "landsby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
                 "lokalsamfunn", "nabolag", 
                 "oslo", "bergen", "trondheim", "stavanger", "tromsø",
                 ]
                 #"community" dropped as causes only noise
                 #added major Norwegian city names, adds no results to phrase 1 but quite a lot to phrase 2

termlist11_6c = ["city", "urban.*"] 


phrasedefault11_6a = r'(?:{})'.format('|'.join(termlist11_6a))
phrasedefault11_6b = r'(?:{})'.format('|'.join(termlist11_6b))
phrasedefault11_6c = r'\b(?:{})\b'.format('|'.join(termlist11_6c))
```


```python
#Search 1
Data.loc[(
     (Data['result_title'].str.contains(phrasedefault11_6a, na=False, case=False))
     & 
      (
         (Data['result_title'].str.contains(phrasedefault11_6b, na=False, case=False))
         |(Data['result_title'].str.contains(phrasedefault11_6c, na=False, case=False))
      )
),"tempsdg11_06"] = "SDG11_06"

print("Number of results = ", len(Data[(Data.tempsdg11_06 == "SDG11_06")])) 
```


```python
test=Data.loc[(Data.tempsdg11_06 == "SDG11_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Term lists
termlist11_6d = ["smog", "air pollution","suspended particles","particulate matter","pm2.5","pm10","clean air","air quality",
                 "luftforure","luftureining","svevestøv","partikler i luft","ren luft","rein luft","luftkvalitet",]
termlist11_6not = ["Cosmogenic"]

phrasedefault11_6d = r'(?:{})'.format('|'.join(termlist11_6d))
phrasedefault11_6not = r'(?:{})'.format('|'.join(termlist11_6not))
#Re-use b and c
```


```python
#Search 2
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault11_6d, na=False, case=False))
    & 
    ((Data['result_title'].str.contains(phrasedefault11_6b, na=False, case=False))
     |(Data['result_title'].str.contains(phrasedefault11_6c, na=False, case=False))
    )
    & (~Data['result_title'].str.contains(phrasedefault11_6not, na=False, case=False))
),"tempsdg11_06"] = "SDG11_06"

print("Number of results = ", len(Data[(Data.tempsdg11_06 == "SDG11_06")])) 
```


```python
test=Data.loc[(Data.tempsdg11_06 == "SDG11_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Term lists

termlist11_6e = ["solid waste", "bulky waste","houshold waste","domestic waste","commercial waste","industrial waste","MSW",
                 "EOL waste","end of life waste","end of chain waste","eoc waste","garbage","rubbish", "composting",
                 
                 "avfall", "søppel", "boss", "komposter"
                 ]
 
phrasedefault11_6e = r'(?:{})'.format('|'.join(termlist11_6e))
#Re-use b and c
```


```python
#Search 3

phrase11_6ebc = Data.loc[(
     (Data['result_title'].str.contains(phrasedefault11_6e, na=False, case=False))
     & 
     (
         (Data['result_title'].str.contains(phrasedefault11_6b, na=False, case=False))
         |(Data['result_title'].str.contains(phrasedefault11_6c, na=False, case=False))
     )
),"tempsdg11_06"] = "SDG11_06"

print("Number of results = ", len(Data[(Data.tempsdg11_06 == "SDG11_06")])) 
```


```python
test=Data.loc[(Data.tempsdg11_06 == "SDG11_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4


```python
#Term lists

termlist11_6f = ["environmental impact", "impact on the environment", "impacts on the environment","environmental assess", "footprint","foot print",
                 "miljøpåvirk", "fotavtrykk", "påvirke miljø", "påverke miljø", "miljøvurdering"]
  
termlist11_6g = ["waste", "garbage", "rubbish", 
                 "avfall", "søppel", "boss"]

termlist11_6h = ["manag", "collect", "reuse", "re-use", "composting", "biological degrad",
                 "håndter", "handter", "innsamling", "samle inn", "gjennvin", "gjenbruk", "resirkuler", "renovasjon", "komposter", "forbrenn", "energi", "deponi"]

phrasedefault11_6f = r'(?:{})'.format('|'.join(termlist11_6f))
phrasedefault11_6g = r'(?:{})'.format('|'.join(termlist11_6g))
phrasedefault11_6h = r'\b(?:{})\b'.format('|'.join(termlist11_6h))
```


```python
#Search 4
phrase11_6fgh = Data.loc[(
    (Data['result_title'].str.contains(phrasedefault11_6f, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault11_6g, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault11_6h, na=False, case=False))   
),"tempsdg11_06"] = "SDG11_06"

print("Number of results = ", len(Data[(Data.tempsdg11_06 == "SDG11_06")])) 
```


```python
test=Data.loc[(Data.tempsdg11_06 == "SDG11_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.7

*By 2030, provide universal access to safe, inclusive and accessible, green and public spaces, in particular for women and children, older persons and persons with disabilities*

*Innen 2030 sørge for at alle, særlig kvinner og barn, eldre og personer med nedsatt funksjonsevne, har tilgang til trygge, inkluderende og tilgjengelige grøntområder og offentlige rom*

#### Phrase 1


```python
#Termlists
termlist11_7a = ["safe", "inclus", "access", "unrestrict",
                 "trygg", "sikker", "inkluder", "inklus", "tilgang", "adgang", "uhindr", "ubegrens"]

termlist11_7b = ["green space", "recreational area", 
                 "public area", "public space", "public open space", "public playground", 
                 "public facilit", "boulevard", "public market",
                 "library area", "library space", "libraries", "public library", "community cent", "community space", "civic cent",
                 "public garden", "community garden", "allotment garden", "urban allotment",

                 "grønne område", "grøntområde", "parkområde", "friluftsområde", "fritidsområde", 
                 "offentleg område", "offentlig område" "offentlig sted", "offentleg stad", "offentlig plass", "offentleg plass", "byrom", "fellesrom",
                 "offentlig fasilit", "offentleg fasilit",
                 "bibliotekareal", "bibliotekrom", "bibliotekbygg", "offentlig bibliotek", "samfunnshus", "forsamlingshus",
                 "bypark", "kolonihage", "parsellhage", "hageparsell", "felleshage"
                 ]

termlist11_7c = ["park", "parks", "street", "avenue", "square", "beach", "waterfront", "riverbank" 
                 "gate", "torg", "strand", "vannkant", "elvebredd",]

termlist11_7d =  ["cities","city", "megacit", "urban", "metropolitan",
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "community", "neighborhood", "neighbourhood", 

                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "landsby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad", "offentlig lekeplass", "offentleg leikeplass",
                 "samfunn", "lokalsamfunn", "nabolag", 
                 "oslo", "bergen", "trondheim", "stavanger", "tromsø",
                 ]

phrasedefault11_7a = r'(?:{})'.format('|'.join(termlist11_7a))
phrasedefault11_7b = r'(?:{})'.format('|'.join(termlist11_7b))
phrasedefault11_7c = r'\b(?:{})\b'.format('|'.join(termlist11_7c))
phrasedefault11_7d = r'(?:{})'.format('|'.join(termlist11_7d))
```


```python
#Search 11_7
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault11_7a, na=False, case=False))
    &
    (   
        (Data['result_title'].str.contains(phrasedefault11_7b, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault11_7c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_7d, na=False, case=False)))
    )              
),"tempsdg11_07"] = "SDG11_07"

print("Number of results = ", len(Data[(Data.tempsdg11_07 == "SDG11_07")])) 
```


```python
test=Data.loc[(Data.tempsdg11_07 == "SDG11_07"), ("result_id", "result_title")]
test.iloc[0:25, ]
```

#### Phrase 2

Here, as it is a title search, we have decided to drop the combination of "parks" + "cities", so that "parks" can be alone. May increase results about e.g. national parks.


```python
#Termlists
termlist11_7e = ["restrict", "inaccess", "equal access", "inequalit", "equit", "justice", 
                 "discriminat", "exclud", "harass", "assault", "unsafe",
                 
                 "restrik", "utilgjenge", "allmen tilgang", "allmenn adgang", "lik adgang", "lik tilgang", "uhindr", "ubegrens", "ulikhet", "rettferd", 
                 "diskrimin", "utesteng", "utenforskap", "eksklude", "trakasser", "mobb", "overfall", "angrep", "utrygg"
                 ]
#"equit" will find "inequitable", "justice" will find "injustice" etc.
phrasedefault11_7e = r'(?:{})'.format('|'.join(termlist11_7e))
```


```python
#Search 11_7
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault11_7e, na=False, case=False))
    &
             (   (Data['result_title'].str.contains(phrasedefault11_7b, na=False, case=False))
             |
               (
                   (Data['result_title'].str.contains(phrasedefault11_7c, na=False, case=False))
                   #& ((Data['result_title'].str.contains(phrasedefault11_7d, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault11_7dtrunc, na=False, case=False)))
               )
             )              
),"tempsdg11_07"] = "SDG11_07"
#Here, as it is a title search, we have decided to drop the combination of "parks" + "cities", so that "parks" can be alone.

print("Number of results = ", len(Data[(Data.tempsdg11_07 == "SDG11_07")])) 
```


```python
test=Data.loc[(Data.tempsdg11_07 == "SDG11_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.a

*Support positive economic, social and environmental links between urban, peri-urban and rural areas by strengthening national and regional development planning*

*Støtte positive økonomiske, sosiale og miljømessige forbindelser mellom byområder, omland og spredtbygde områder ved  å styrke nasjonale og regionale planer*


```python
#Termlists
termlist11_Aa = ["national", "regional",
                 "nasjonal", "landsdek"]
termlist11_Ab = ["plan", "strateg", "framework", "program", "policy", "policies", "cooperat",
                 "rammeverk", "styring", "politikk", "politisk", "samarbeid", "koopera"]

termlist11_Ac =   ["cities", "megacit", "urban", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "settlement", "built-up area", "populated area",
                 "local community", "neighborhood", "neighbourhood", 
                 "rural area", "rural development",

                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "landsby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
                 "lokal samfunn", "lokalsamfunn", "nabolag", 
                 "rural utvikling", "bypolit",
                 ]
                 #City names mostly cause noise here so are not included

termlist11_Actrunc = ["city"] #"city" is here due to capaCITY

phrasedefault11_Aa = r'(?:{})'.format('|'.join(termlist11_Aa))
phrasedefault11_Ab = r'(?:{})'.format('|'.join(termlist11_Ab))
phrasedefault11_Ac = r'(?:{})'.format('|'.join(termlist11_Ac))
phrasespecific11_Actrunc = r'\b(?:{})\b'.format('|'.join(termlist11_Actrunc))
```


```python
#Search 11_A
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault11_Aa, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault11_Ab, na=False, case=False))
    & ((Data['result_title'].str.contains(phrasedefault11_Ac, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific11_Actrunc, na=False, case=False)))
),"tempsdg11_a"] = "SDG11_0a"

print("Number of results = ", len(Data[(Data.tempsdg11_a == "SDG11_0a")]))  
```


```python
test=Data.loc[(Data.tempsdg11_a == "SDG11_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.b

*By 2020, substantially increase the number of cities and human settlements adopting and implementing integrated policies and plans towards inclusion, resource efficiency, mitigation and adaptation to climate change, resilience to disasters, and develop and implement, in line with the Sendai Framework for Disaster Risk Reduction 2015–2030, holistic disaster risk management at all levels*

*Innen 2020 oppnå en betydelig økning i antall byer og lokalsamfunn som vedtar en integrert politikk og gjennomfører planer med  sikte  på inkludering, bedre ressursbruk, begrensning av og tilpasning til klimaendringer samt evne til å stå imot og håndtere katastrofer, og dessuten utvikle og iverksette et helhetlig system for risikostyring og katastrofehåndtering på alle nivå, i tråd med Sendai-rammeverket for katastrofeberedskap for 2015–2030*


```python
#Termlists
termlist11_Ba = ["sendai", "disaster risk reduction", "cancun adapation framework", "readiness and preparatory support programme", "readiness programme",
                 "katastrofeforebygging", "cancun-avtal", "cancun avtal", "klimatilpas", "forebyggingstiltak"
                 ]
termlist11_Bb = ["plan ", "plans", "planning", "strateg", "program", "policy", "policies", "governance", "framework", "preparedness",
                 "rammeverk", "politikk", "politisk", "forvalt", "styring", "ledelse", "leiing", "retningslin", "forebygg", "beredskap",
                 ]
                 #space after "plan" to prevent "plant"
termlist11_Bc = ["disaster", "risk judgement", "climate change", "climatic change", "global warming", "changing climate", "climate action", "climate mitigation", 
                 "katastrofe", "klimaendring", "global oppvarming", "klimatiltak", "klimatilpas"
                 ]
                 #dropped "risk"/ "risiko" (NO) - to drop results about chemical risk assessments/risks in health and animals. Used "risk judgements"
termlist11_Bd = ["settlement", 
                 "cities", "megacit", "urban", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "neighborhood", "neighbourhood", 
                 "local communit", 

                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
                 "bosetting", "busetting", 
                 "nabolag", 
                 "lokal samfunn",
                 "oslo", "bergen", "trondheim", "stavanger", "tromsø",
                 ]
termlist11_Bdtrunc = ["city"] #"city" is here due to toxiCITY

phrasedefault11_Ba = r'(?:{})'.format('|'.join(termlist11_Ba))
phrasedefault11_Bb = r'(?:{})'.format('|'.join(termlist11_Bb))
phrasedefault11_Bc = r'(?:{})'.format('|'.join(termlist11_Bc))
phrasedefault11_Bd = r'(?:{})'.format('|'.join(termlist11_Bd))
phrasespecific11_Bdtrunc = r'\b(?:{})\b'.format('|'.join(termlist11_Bdtrunc))
#"klimatilpas"(NO) in termlist Bc is probably redundant, as it is included in Ba
```


```python
#Search 11_B
Data.loc[(
             (   (Data['result_title'].str.contains(phrasedefault11_Ba, na=False, case=False))
             |    
               ( (Data['result_title'].str.contains(phrasedefault11_Bb, na=False, case=False))
               & (Data['result_title'].str.contains(phrasedefault11_Bc, na=False, case=False))
               )
             )
             & ((Data['result_title'].str.contains(phrasedefault11_Bd, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific11_Bdtrunc, na=False, case=False)))           
),"tempsdg11_b"] = "SDG11_b"

print("Number of results = ", len(Data[(Data.tempsdg11_b == "SDG11_b")]))  
```


```python
test=Data.loc[(Data.tempsdg11_b == "SDG11_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.c

*Support least developed countries, including through financial and technical assistance, in building sustainable and resilient buildings utilizing local materials*

*Bistå de minst utviklede landene med å oppføre bærekraftige og solide bygg ved bruk av lokale materialer, blant annet   gjennom  økonomisk og faglig bistand*




```python
#Term lists

termlist11_Ca = ["sustainable architecture","resilient architecture","Sustainable Building and Construction Initiative","sustainable building","sustainable construction",
                 "local building material", "local construction material", "locally available building material",
                 
                 "bærekraftig arkitektur","berekraftig arkitektur","bærekraftig bygning","berekraftig bygning","bærekraftig konstruksjon", "berekraftig konstruksjon",
                 "lokale bygningsmatrial","lokale konstruksjonsmaterial"] 
  
termlist11_Cb = ["sustainable", "green", "eco-", "ecofriendly", "environmentally friendly", "resili",
                 "local material", "locally available", "native", "traditional",
                 
                 "bærekraftig", "berekraftig", "grøn", "miljøven", "økoven", "tradisjonel", "lokal"]

termlist11_Cc = ["construction", "buildings", "building material", "building technique", "building method", "building industry", "home building", "building homes",
                 "konstruksjon", "bygge", "byggningsbransj", "byggebransj"]
                 #"building" causes issues (capacity building etc.)
    
termlist11_Cd_case = ["SBCI"]

phrasedefault11_Ca = r'(?:{})'.format('|'.join(termlist11_Ca))
phrasedefault11_Cb = r'(?:{})'.format('|'.join(termlist11_Cb))
phrasedefault11_Cc = r'(?:{})'.format('|'.join(termlist11_Cc))
phrasedefault11_Cd_case = r'\b(?:{})\b'.format('|'.join(termlist11_Cd_case))
```


```python
#Search 1 - in LDCs
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault11_Ca, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault11_Cb, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault11_Cc, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault11_Cd_case, na=False, case=False))
    )
    & (Data['LDCs']==True)
),"tempsdg11_c"] = "SDG11_c"

print("Number of results = ", len(Data[(Data.tempsdg11_c == "SDG11_c")]))
```


```python
test=Data.loc[(Data.tempsdg11_c == "SDG11_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11 mentions

Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 


```python
#Termlists
termlist11_1 = ["SDG 11", "SDGs 11", "SDG11", "sustainable development goal 11", 
               "bærekraftsmål 11", "berekraftsmål 11"]
termlist11_2 = ["sustainable development goal", 
               "bærekraftsmål", "berekraftsmål"]
termlist11_3 = ["goal 11", "mål 11"]
termlist11_4 = ["sustainable development goal", "SDG", "goal 11", 
               "bærekraftsmål", "berekraftsmål", "mål 11"]
termlist11_5 = ["cities", 
               "byer", "byar"]
termlist11_6 = ["sustainable cities and communities" 
                "bærekraftige byer og lokalsamfunn"]
#Possible search for the short titles of the SDGs, to be used in a title search

phrasedefault11_1 = r'(?:{})'.format('|'.join(termlist11_1))
phrasedefault11_2 = r'(?:{})'.format('|'.join(termlist11_2))
phrasedefault11_3 = r'(?:{})'.format('|'.join(termlist11_3))
phrasedefault11_4 = r'(?:{})'.format('|'.join(termlist11_4))
phrasedefault11_5 = r'(?:{})'.format('|'.join(termlist11_5))
phrasedefault11_6 = r'(?:{})'.format('|'.join(termlist11_6))
```


```python
#search
Data.loc[(
      (Data['result_title'].str.contains(phrasedefault11_1, na=False, case=False))
      |(Data['result_title'].str.contains(phrasedefault11_6, na=False, case=False))
      |
      (
        (Data['result_title'].str.contains(phrasedefault11_2, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault11_3, na=False, case=False))
      )
      |
      (
         (Data['result_title'].str.contains(phrasedefault11_4, na=False, case=False))
         & (Data['result_title'].str.contains(phrasedefault11_5, na=False, case=False))
      )
),"tempmentionsdg11"] = "SDG11"

print("Number of results = ", len(Data[(Data.tempmentionsdg11 == "SDG11")]))
```


```python
test=Data.loc[(Data.tempmentionsdg11 == "SDG11"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 12

### SDG 12 - sutainable consumption and production string

In SDG12, there is a string often re-used/modified to specify sustainable consumption and production. This is included here and reused in targets as needed (currently 4 targets, 12.1, 12.2, 12.6, 12.a, in an unmodified form). 


```python
#Term lists
termlist12_scp1 = ["ecobuilding", "eco-building", "eco-housing", "eco-construct", "eco-design", "eco-technolog",
                   "green building", "green housing", "green construct", "green design", "green technolog",
                   "sustainable building", "sustainable housing", "sustainable construct", "sustainable design", "sustainable technolog",
                   "Sustainable Building and Construction Initiative", "SCBI",
                   "sustainable lifestyle" , "sustainable life style" , "green lifestyle" , "eco-lifestyle" , "environmental lifestyle",
                   "ecolabel", "eco-label", 
                   "ecotourism", "eco-tourism",
                   "responsible consump", "cleaner production",
                   "circular econom", "circular bioeconom", "circular product", "circular consumption",
                   "lifecycle analys", "lifecycle assess", "material lifecycle",
                   "cradle-to-cradle", "cradle to cradle",
                   
                   "bærekraftig liv", "berekraftig liv", "grønn livsstil", "miljøvennlig hverdag", "miljøvennlig liv",
                   "miljømerk", "svanemerk",
                   "økoturism",
                   "ansvarlig forbruk", "ansvarleg forbruk", "renere produksjon",
                   "sirkulær økonomi", "sirkulær bioøkonomi", "sirkulær produk", "sirkulær forbruk", 
                   "livssyklusanalyse", "livsløpsvurdering",
                   "vugge til vugge"
                  ]
# In Norwegian, the construction terms (translations of ecobuilding etc.) are added to the phrase below as it needs more flexibility in this language
# Svanemerk is a Norwegian ecolabelling scheme

termlist12_scp2_trunc = ["green", "eco", "eco-.*", "sustainab.*", "responsib.*", "environmental.*", "ecological.*",
                         "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "ansvarlig.*", "miljø.*"
                        ]
# truncated as "eco" causes noise if not
#"Grønn" (NO) is truncated to avoid "grønnsak"
termlist12_scp3 = ["consumer", 
                   "certificat", "label",
                   "tourism", "tourist", "travel", "hospitality", "leisure",
                   
                   "forbruk", "kunder",
                   "stempel", "akkredit", "sertifi", "merke", "merking",
                   "turism", "turist", "reise", "fritid",
                   "bygg", "bolig", "materialer"]
#will find e.g. "miljøsertifisering" (NO)

termlist12_scp4_trunc = ["utili.*", "use", "usage", "using", "design.*",
                         "bruk.*", "forbruk"]

termlist12_scp5 = ["sidestream", "side-stream", "byproduct", "by-product"
                  "sidestrøm", "biprodukt"]

termlist12_scp6 = ["recycl", "reuse", "re-use", "reusing", "re-using", "refurbish", "re-furbish", "remanufactur", "re-manufactur", "repurpos", "re-purpos",
                   "compost", "codigest", "co-digest",
                   "resource efficien", "resource-use efficien", "material efficicen", "material-use efficien", "footprint",
                   
                   "resirkul", "gjenbruk", "ombruk",
                   "kompost",
                   "ressurseffektiv", "materialeffektiv", "effektiv bruk av material", "effektiv bruk av ressurs", "fotspor"]
termlist12_scp7 = ["bioeconom", "bio-econom", "produc", "consum",
                   "packaging",
                   "sidestream", "side-stream", "byproduct", "by-product"
                   "resource", "material", "matter", "biomass",
                   "waste", "garbage", "trash",
                   
                   "bioøkonom", "produksj", "produkter", "forbruk",
                   "innpakning", "emballasje", "emballering", 
                   "sidestrøm", "biprodukt",
                   "ressurs",
                   "avfall", "søppel", "kloakk", " slam"]

termlist12_scp8_trunc = ["green", "eco", "eco-.*", "sustainab.*", "environmental.*", "ecological.*",
                         "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "miljø.*"]
termlist12_scp9 = ["waste", "garbage", "trash", "rubbish", "litter", "sewage", "sludge",
                   "avfall", "søppel", "kloakk", " slam"
                  ]
termlist12_scp10 = ["management", "handling", "collect", "transport", "storing", "dispos", "treatment", "processing", "sorting", "incinerat", "combust", 
                    "end of life", "end of chain", "end-of-life", "end-of-chain",
                    "packaging", "labelling", 
                    
                    "ledelse", "håndter", "samle", "samling", "oppbevar", "lagring", "avhend", "tømming", "prossess", "sortering", "sortere", "forbrenning",
                    "innpakning", "emballasje", "emballering", "stempel", "akkredit", "sertifi", "merke", "merkering"]
# "behandling" (NO) not included, as mostly seems to result in e.g. "miljøbehandling" in health
termlist12_scp11 = ["footprint"
                    "produc", "consum",
                    "retail", "trade", "market",
                    " handling", "storage", "transport", "distribution network", "packaging", "supply chain", "logistics",
                    "procurement", "aquisition", "purchas", "investment",
                    "resource efficien", "resource-use efficien", "material efficicen", "material-use efficien",
                    "food system", "food production", "food consumption", "food security",
                    "agricultur", "cropping system", "agroforest", "agro-forest", "aquaculture", "fisher", "fish farm",
                    
                    "forspor",
                    "produksj", "forbruk",
                    "marked", "detaljhandel", "faghandel", "dagligvare",
                    "håndter", "innsaml", "samling", "oppbevar", "lagring", "innpakning", "emballasje", "emballering", "forsyningskjede", "logistikk",
                    "anskaffels", "anbud", "innkjøp", "investering",
                    "ressurseffektiv", "materialeffektiv", "effektiv bruk av material", "effektiv bruk av ressurs", 
                    "matsystem", "matproduksjon", "matforbruk", "matsikkerhet",
                    "jordbruk", "landbruk", "havbruk", "fiskeoppdrett"]
# The space in front of "handling" (EN/NO) is necessary to prevent "behandling" in Norwegian. Not needed in other languages potentially.

phrasedefault12_scp1 = r'(?:{})'.format('|'.join(termlist12_scp1))
phrasespecific12_scp2 = r'\b(?:{})\b'.format('|'.join(termlist12_scp2_trunc))
phrasedefault12_scp3 = r'(?:{})'.format('|'.join(termlist12_scp3))
phrasespecific12_scp4 = r'\b(?:{})\b'.format('|'.join(termlist12_scp4_trunc))
phrasedefault12_scp5 = r'(?:{})'.format('|'.join(termlist12_scp5))
phrasedefault12_scp6 = r'(?:{})'.format('|'.join(termlist12_scp6))
phrasedefault12_scp7 = r'(?:{})'.format('|'.join(termlist12_scp7))
phrasespecific12_scp8 = r'\b(?:{})\b'.format('|'.join(termlist12_scp8_trunc))
phrasedefault12_scp9 = r'(?:{})'.format('|'.join(termlist12_scp9))
phrasedefault12_scp10 = r'(?:{})'.format('|'.join(termlist12_scp10))
phrasedefault12_scp11 = r'(?:{})'.format('|'.join(termlist12_scp11))
```


```python
#Search
Data["scp"]=(
    (Data['result_title'].str.contains(phrasedefault12_scp1, na=False, case=False))
    |((Data['result_title'].str.contains(phrasespecific12_scp2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_scp3, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasespecific12_scp4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_scp5, na=False, case=False)))
    |((Data['result_title'].str.contains(phrasedefault12_scp6, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_scp7, na=False, case=False)))
    |
        (
            (Data['result_title'].str.contains(phrasespecific12_scp8, na=False, case=False)) 
            & 
                ((Data['result_title'].str.contains(phrasedefault12_scp11, na=False, case=False))
                 |((Data['result_title'].str.contains(phrasedefault12_scp9, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_scp10, na=False, case=False)))
                )
        )
    )

print("Number of results = ", len(Data.loc[Data['scp']])) 
```


```python
#Results
test=Data.loc[Data['scp']]
test.iloc[0:5, [3,5,6,25,26]]
```

### SDG 12.1

*12.1 Implement the 10‑Year Framework of Programmes on Sustainable Consumption and Production Patterns, all countries taking action, with developed countries taking the lead, taking into account the development and capabilities of developing countries*

*Gjennomføre det tiårige handlingsprogrammet for bærekraftig forbruk og produksjon ved at alle land deltar, men slik at de utviklede landene går foran, samtidig som det tas hensyn til utviklingslandenes utviklingsnivå og muligheter*


```python
#Term lists
#Here in the title search it is simplified, so that `national OR regional...` etc. is not included

termlist12_1a = ["10 year framework of program", "10-year framework of program", "10YFP",
                "handlingsprogrammet for bærekraftig forbruk og produksjon"]

termlist12_1b_trunc = ["polic.*", "govern.*", "action plan.*", "regulat.*", "legal.*", "law", "laws", "legislat.*", "standards", "code of conduct.*", "accounting", "reporting",
                       "politikk.*", "handlingsplan.*", "tiltaksplan.*", "regulasj.*", ".*lovverk.*", "lovgiv.*", "utredning.*", "utgreiing", "standarder", "retningslinje.*", "rapportering.*"]

termlist12_1c_trunc = ["strateg.*", "framework", "program.*", "plan", "plans", "planning", "target.*", "goal.*", "instrument", "instruments", "national standard", "international standard",
                       "rammeverk", "planer", "planar", "planlegg.*", "mål", "nasjonal standard", "internasjonal standard"]

phrasedefault12_1a = r'(?:{})'.format('|'.join(termlist12_1a))
phrasespecific12_1b = r'\b(?:{})\b'.format('|'.join(termlist12_1b_trunc))
phrasespecific12_1c = r'\b(?:{})\b'.format('|'.join(termlist12_1c_trunc))
```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault12_1a, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific12_1b, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific12_1c, na=False, case=False))
    )
    &(Data['scp']==True)
    ),"tempsdg12_01"] = "SDG12_01"

print("Number of results = ", len(Data[(Data.tempsdg12_01 == "SDG12_01")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_01 == "SDG12_01"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.2

*12.2 By 2030, achieve the sustainable management and efficient use of natural resources*

*Innen 2030 oppnå bærekraftig forvaltning og effektiv bruk av naturressurser*


#### Phrase 1


```python
#Termlists

termlist12_2a_trunc = ["eco", "eco-.*", "green", "sustainab.*", "responsibl.*", "environmental.*", "ecological", "long-term management",
                       "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "ansvarlig.*", "miljø.*", "strategisk planlegging", "langsiktig planlegging", "langsiktig ledelse"]

termlist12_2c_trunc = ["manag.*", "extract.*", "practice.*", "resource use", "usage", "consumption", "consume.*",
                       "govern.*", "development", "administrat.*", "plan", "planning", "policy", "policies",
                       
                       "forvalt.*", "høsting", "praksis", "bærekraftig bruk", "berekraftig bruk", "ressursbruk", "bruk av ressurs", "forbruk",
                       "strying.*", "utvikling", "handlingsplan.*", "tiltaksplan.*", "planer", "planar", "planlegg.*", "regulasj.*", "lovverk", "lovgiv.*", "utredning", "utgreiing", "rammeverk", "politikk.*"]

#Terms that already indicate USE of resources (2d) - combined with sustainable/eco etc (2a)
termlist12_2d = ["forestry", 'silvicult', "arboritcult", "logging",
                 "mining",
                 "fishery", "fisheries", "hunting",
                 "water use", "use of water",
                 
                 "skogbruk", "skogskjøtsel", "skogpleie", "skogsvirke",
                 "gruvedrift",
                 "fiskeri", "jakt",
                 "vannbruk", "bruk av ferskvann"]

#Terms that are just resources (2e) - combined with sustainable/eco (2a) and management/extraction (2c).
termlist12_2e = ["natural resource", "natural material", "renewable resource", "renewable material", "natural capital", "raw material", 
                 "forest", "woodland", 
                 "ocean", "marine", "fresh water", "lake", "river", "coastal", "wildlife", 
                 "water supply", "water supplies", "water resource", "freshwater resource", "supply of freshwater", "water management",
                 "mineral",
                 
                 "naturressurs", "naturlige materialer", "fornybar ressurs", "fornybare ressurs", "fornybar material", "fornybare material", "naturkapital", "råvare",
                 "skog",
                 "sjøen", "havet", "ferskvann", "innsjø", 
                 "vannressurs", "vassdrag", "grunnvann", "vannforvalt",
                 "landressurs", "jordressurs"]
termlist12_2e_trunc = ["land", "soil", "soils", "metal", "metals", "ore", "ores",
                       "sjø", "hav", "kyst", "kysten", "jord", ".*malm", "malmer"]

termlist12_2f = ["global forest goals", "forest under certification", "certified forest area", "international resource panel",
                "strategiske plan for skog", "sertifisering av skog", "skog sertifisering", "internasjonale ressurspanelet"]

phrasespecific12_2a = r'\b(?:{})\b'.format('|'.join(termlist12_2a_trunc))
phrasespecific12_2c = r'\b(?:{})\b'.format('|'.join(termlist12_2c_trunc))
phrasedefault12_2d = r'(?:{})'.format('|'.join(termlist12_2d))
phrasedefault12_2e = r'(?:{})'.format('|'.join(termlist12_2e))
phrasespecific12_2e = r'\b(?:{})\b'.format('|'.join(termlist12_2e_trunc))
phrasedefault12_2f = r'(?:{})'.format('|'.join(termlist12_2f))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault12_2f, na=False, case=False))
    |((Data['result_title'].str.contains(phrasespecific12_2a, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_2d, na=False, case=False)))
    |
    (
        (Data['result_title'].str.contains(phrasespecific12_2a, na=False, case=False))
        & (Data['result_title'].str.contains(phrasespecific12_2c, na=False, case=False))
        & ((Data['result_title'].str.contains(phrasedefault12_2e, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific12_2e, na=False, case=False)))
    )
    ),"tempsdg12_02"] = "SDG12_02"

print("Number of results = ", len(Data[(Data.tempsdg12_02 == "SDG12_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_02 == "SDG12_02"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
#Here we reuse the natural resources and management/use terms from phrase 1 (but note that this phrase also includes terms for some unsustaibable natural resources)

termlist12_2g = ["unsustainab", "irresponsib", "unecological", "inefficien",
                 "ubærekraftig", "uansvarlig", "ueffektiv"]

termlist12_2h_trunc = ["fossil fuel.*", "coal", "oil", "natural gas", "peat", "diesel", "gasoline", "kerosene", "petroleum", "energy resource.*",
                       "fossilt brensel.*", "fossile brensl.*", "fossilt brennstoff.*", "fossile brennstoff.*", "kull", "olje", "naturgass", "parafin.*", "energiressurs.*"]

phrasedefault12_2g = r'(?:{})'.format('|'.join(termlist12_2g))
phrasespecific12_2h = r'\b(?:{})\b'.format('|'.join(termlist12_2h_trunc))
```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault12_2d, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasespecific12_2c, na=False, case=False))
            & 
            ((Data['result_title'].str.contains(phrasedefault12_2e, na=False, case=False))
             |(Data['result_title'].str.contains(phrasespecific12_2e, na=False, case=False))
             |(Data['result_title'].str.contains(phrasespecific12_2h, na=False, case=False))
            )
        )
    )
    & (Data['result_title'].str.contains(phrasedefault12_2g, na=False, case=False))
    ),"tempsdg12_02"] = "SDG12_02"

print("Number of results = ", len(Data[(Data.tempsdg12_02 == "SDG12_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_02 == "SDG12_02"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
#Here we reuse the parts/all of the scp string, even though it is slightly wider than the original WoS combination string
#In addition, there are two other new elements added:
# "efficient use" (in WOS = ("saving" OR "save$" OR "conserv*" OR "efficien*") NEAR/5 ("use" OR "using" OR "usage" OR "utili*" OR "consumption"))
# circular economy (stands alone without having to mention natural resources in WOS)
#And combine it with the natural resources strings in phrase 1

termlist12_2i = ["circular econom", "circular bioeconom", "circular product", "circular consumption",
                 "material lifecycle", "material footprint",
                 
                 "sirkulær økonomi", "sirkulær bioøkonomi", "sirkulær produk", "sirkulær forbruk",
                 "materialets livssyklus", "materialenes livssyklus"]

termlist12_2j = ["efficient consum", "efficient us", "conservative us",
                 "effektiv forbruk", "effektiv bruk", "sparsom"]

phrasedefault12_2i = r'(?:{})'.format('|'.join(termlist12_2i))
phrasedefault12_2j = r'(?:{})'.format('|'.join(termlist12_2j))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault12_2i, na=False, case=False))
    | ((Data['result_title'].str.contains(phrasedefault12_scp6, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_scp7, na=False, case=False)))
    |
    (
        ((Data['result_title'].str.contains(phrasedefault12_2d, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific12_2e, na=False, case=False))
        |(Data['result_title'].str.contains(phrasedefault12_2e, na=False, case=False))
        )
        & ((Data['scp']==True)|(Data['result_title'].str.contains(phrasedefault12_2j, na=False, case=False)))
    )
    ),"tempsdg12_02"] = "SDG12_02"

print("Number of results = ", len(Data[(Data.tempsdg12_02 == "SDG12_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_02 == "SDG12_02"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:10, ]
```

#### Phrase 4


```python
#Termlists
#Here we reuse the natural resources strings in phrase 1/2, but some more of the terms are combined with "resources" 
#(to avoid being too general, e.g. "loss + land" is forced to "loss + land + resources")

#As this is a title search, we do not include the "reduce" element - so it is expanded to be about consumption generally

termlist12_2k = ["resource", "material",
                 "ressurs"]

termlist12_2l_trunc = ["material footprint", "material consumption", "ecological footprint", "resource footprint",
                       "reduce the us", "decrease the us", "reduce usage", "decrease usage",
                       "extract", "extraction", "consum.*", 
                       "deplet.*", "exploit.*", 
                       "waste", "loss", 
                       
                       ".*fotspor", 
                       "reduserer bruk",
                       "ekstrak.*", "forbruk", "uttømm.*", 
                       "svinn", "avfall", "tap"]
#"using" caused a lot of noise, many results about for example "Examining resource x USING method y", and not actually about use of the resource.
# Extraction is specified as "extracts" gives results from oil extracts

phrasedefault12_2k = r'(?:{})'.format('|'.join(termlist12_2k))
phrasespecific12_2l = r'\b(?:{})\b'.format('|'.join(termlist12_2l_trunc))
```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault12_2d, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault12_2e, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_2k, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasespecific12_2e, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_2k, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasespecific12_2h, na=False, case=False))
    )
    & (Data['result_title'].str.contains(phrasespecific12_2l, na=False, case=False))
    ),"tempsdg12_02"] = "SDG12_02"

print("Number of results = ", len(Data[(Data.tempsdg12_02 == "SDG12_02")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_02 == "SDG12_02"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 5

Note - this is identical to 2.4 phrase 4


```python
termlist12_2m = ["food-produc", "food produc", "grower", "agrifood", "agri-food", "agro-food", "agro food",
                "agricultur", "farm", "smallhold", "small-hold", "permacultur", "cropping", "orchard", "arable land",
                "pasture", "pastoral", "agroforest", "agro-forest", "silvopastur", "silvopastoral",
                "aquacultur", "maricultur", "fisher", "fish farm", "herding",
                "crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", "legume",
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                "fodder", "animal feed ", "fish feed ",
                
                "matproduksjon", "matprodusent",
                "gård", "gard", "landbruk", "jordbruk", "gårdsbruk", "gardsbruk", "småbruk", "familiebruk", "dyrket mark", "dyrkamark",
                "dyrka mark", "kultivert mark",
                "beite", "dyreproduksjon", "meieri",
                "fiskeoppdrett", "lakseoppdrett", "havbruk",
                "grønnsak", "grønsak", "belgfrukt", "frukt", "fiske", "laks", " sau ", "sauedrift", "sauehold", "storfe", " svin", "fjærkre", " rein",
                "bærekraftig fôr", "berekraftig fôr", "dyrefôr", "dyrefor ", "fiskefôr", "fiskefor "]
                #Space before " rice" to avoid "price", similarly "sau/svin" (NO) and after "xxxfor" (NO, to avoid "forbund" etc.). Note that "agricultur" will also cover e.g. "ecoagriculture"
    
termlist12_2n = ["ecoagricultur", "eco-agricultur", "agroecolog", "permaculture", "conservation agriculture", "conservation farming",
                "organic farm", "organic agricult", "organic crop", "organic orchard", "organic arable", "organic pasture",
                "organic aquacultur", "organic salmon", "organic pig", "organic poultry", "organic dairy", "organic reindeer",

                "økolandbruk", "økojordbruk", "permakultur"]
                #"organic" is not used alone, but is instead combined in phrases to avoid e.g. organic acids, organic matter. Moved to this part rather than 4j as it can stand alone.
                #"bærekraftig fôr" (NO) is added specifically due to it's inclusion as a priority area ("samfunnsoppdrag") in the governments Long-term plan.
              
termlist12_2o = ["sustainab", "eco-friendly", "environmentally friendly", "ecosystem approach", "ecosystem based",
                "natural pest control", "natural pest management", "biological pest control", "intergrated pest management",
                "intercropping", "cover crop", "crop rotation", "polyculture", "permaculture", 
                "reduced tillage", "mulch", "mulching",
                "water conservation",

                "bærekraftig", "berekraftig", "selvbærende", "sjølvberande", "miljøvennlig", "miljøvennleg", "miljøvenleg", "miljøbevisst", "miljømedveten", "miljømedviten", "økosystem", 
                "økologisk", "biologisk bekjempelse", "biologisk nedkjemping", "biologisk skadedyrkontroll", "integrert skadedyrkontroll", "integrert ugrasbekjempelse", "integrert plantevern",
                "vekstskifte", "grønngjødsling", "dekkvekst", "underkultur", "underså", "ettervekster", "polykultur", "permakultur",
                "redusert jordarbeiding", "gjødselplanlegging",
                "vannsparing"                ] 

phrasedefault12_2m = r'(?:{})'.format('|'.join(termlist12_2m))
phrasedefault12_2n = r'(?:{})'.format('|'.join(termlist12_2n))
phrasedefault12_2o = r'(?:{})'.format('|'.join(termlist12_2o))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault12_2n, na=False, case=False)) 
    | ((Data['result_title'].str.contains(phrasedefault12_2m, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_2o, na=False, case=False)))
    ),"tempsdg12_02"] = "SDG12_02"

print("Number of results = ", len(Data[(Data.tempsdg12_02 == "SDG12_02")])) 
```

### SDG 12.3

*12.3 By 2030, halve per capita global food waste at the retail and consumer levels and reduce food losses along production and supply chains, including post-harvest losses*

*Innen 2030 halvere matsvinn per innbygger på verdensbasis, både i detaljhandelen og blant forbrukere, og redusere svinn i produksjons- og forsyningskjeden, inkludert svinn etter innhøsting*


#### Phrase 1


```python
#Termlists

termlist12_3a = ["food", "fodder"
                 "matvare", "matprodukt", "matsvinn", "matprodu", "bærekraftig fôr", "berekraftig fôr", "dyrefôr", "fiskefôr"]

termlist12_3a_trunc = ["animal feed", "fish feed", 
                       "mat", "dyrefor", "fiskefor"]

termlist12_3b_trunc = ["loss", "losses", "lost", "waste", "wastage", "spoil.*", "discard.*", "incinerat.*", "perish.*",
                       "matsvinn.*", "svinn.*", "tap", "tapt", "avfall", "søppel", "kaste.*", "går til spille", "går til grunne"]
#This works ok without the NOT phrase in a title search

phrasedefault12_3a = r'(?:{})'.format('|'.join(termlist12_3a))
phrasespecific12_3a = r'\b(?:{})\b'.format('|'.join(termlist12_3a_trunc))
phrasespecific12_3b = r'\b(?:{})\b'.format('|'.join(termlist12_3b_trunc))
```


```python
#Search
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault12_3a, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific12_3a, na=False, case=False)))
    &(Data['result_title'].str.contains(phrasespecific12_3b, na=False, case=False))
),"tempsdg12_03"] = "SDG12_03"

print("Number of results = ", len(Data[(Data.tempsdg12_03 == "SDG12_03")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_03 == "SDG12_03"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
#Re-use the "loss" terms from phrase 1 (phrasespecific12_3b)

termlist12_3c = ["cereal", "pulses", "fruit", "berry", "berries", "vegetable", "soybean", "lentil", "chickpea", "legume",
                 "grain", "wheat", "maize", "livestock", "cattle", "sheep", "poultry", "goat", "chicken", "buffalo",
                 "dairy waste", "slaughter",
                 "harvest", 
                 
                 "grønnsak", "grønsak", "frukt", 
                 "oppdrettslaks", "oppdrett", "storfe", "fjærkre",
                 "dyreproduksjon", "meieri", "slakt",
                 "innhøst", "høsting"]

termlist12_3c_trunc = ["crop", "crops", "rice", "fisher.*", "pig", "pigs", "duck", "milk",
                       "sau", "sauer", "sauedrift", "geit", "geiter", "svin", "svinedrift", "rein", "reindrift", "melk", "fiske.*"]

termlist12_3d = ["production", "processing", " handling", "storage", "transport", "distribution", "market", "packaging", "supply chain", "logistics",
                 "retail", "food service", "food service", "restaurant", "household", "farm", 
                 "consumer", "consumption", "consume", 
                 "harvest", "slaughter",
                 
                 "produksjon", "håndter", "innsaml", "samling", "oppbevar", "lagring", "innpakning", "emballasje", "prossess", "innpakning", "emballasje", "emballering", "forsyningskjede", "logistikk",            
                 "matindustri", "matvare", "dagligvare", "hushold", "gård",
                 "forbruk",
                 "innhøst", "høsting", "slakt"]

phrasedefault12_3c = r'(?:{})'.format('|'.join(termlist12_3c))
phrasespecific12_3c = r'\b(?:{})\b'.format('|'.join(termlist12_3c_trunc))
phrasedefault12_3d = r'(?:{})'.format('|'.join(termlist12_3d))
```


```python
#Search
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault12_3c, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific12_3c, na=False, case=False)))
    & (Data['result_title'].str.contains(phrasedefault12_3d, na=False, case=False))
    & (Data['result_title'].str.contains(phrasespecific12_3b, na=False, case=False))
    ),"tempsdg12_03"] = "SDG12_03"

print("Number of results = ", len(Data[(Data.tempsdg12_03 == "SDG12_03")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_03 == "SDG12_03"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.4

*12.4 By 2020, achieve the environmentally sound management of chemicals and all wastes throughout their life cycle, in accordance with agreed international frameworks, and significantly reduce their release to air, water and soil in order to minimize their adverse impacts on human health and the environment*

*Innen 2020 oppnå en mer miljøvennlig forvaltning av kjemikalier og alle former for avfall gjennom hele livssyklusen, i samsvar med internasjonalt vedtatte rammeverk, og betydelig redusere utslipp av kjemikalier og avfall til luft, vann og jord for mest mulig å begrense skadevirkningene for folkehelsen og for miljøet*


#### Phrase 1 (& 5)
Note that this will also cover phrase 5 wos string, which uses the terms `"unsustainab*" OR "irresponsib*" OR "unecological*" OR "unsafe"` (covered by truncation here).


```python
#Termlists

termlist12_4a_trunc = [".*sustainab.*", ".*responsib.*", "environmental.*", ".*ecological.*", "eco", "eco-.*", "green", "safe", "unsafe", "safely", "safety",
                       "bærekraft.*", "berekraft.*", "ubærekraftig", "ansvarlig.*", "uansvarlig", "grønne.*", "grønn", "øko", "miljø.*", "trygg", "utrygg", "sikker.*"]

termlist12_4b_trunc = ["life cycle.*", "lifecycle.*", "end of life", "end of chain",
                       "management", "handling", "packaging", "labelling", "storing", "storage", "stored",
                       "disposal", "dispose", "transport.*", "process.*", "logistics",
                       "use", "uses", "usage", "using", "utilis.*", "utiliz.*", "production",
                       
                       "livssyklus.*", "livløp.*", 
                       "håndter.*", "innsaml.*", "samling", "innpakning", "emballasje", "emballering", "stempel", "merking", "akkredit.*", "sertifi.*", "oppbevar.*", "lagring", 
                       "avhend.*", "tømming", "prossess", "forsyningskjede", "logistikk",
                       "forbruk", "bruk", "produksjon"]

termlist12_4b = ["life cycle analysis", "lifecycle analysis", "cradle to cradle", "cradle-to-cradle",
                 "livssyklusanalyser", "livsløpsanalyser", "vugge til vugge"]

termlist12_4c = ["chemical", "polish", "cleaning product", "engine oil", "plastic", "nanomaterial", 
                 "pesticid", "herbicide", "insecticide", "fungicide",
                 "solvent", "etching solution", "battery", "batteries", "accumulator",
                 "medicinal residue", "toxic mould",
                 "Antimony", "Arsenic", "Beryllium", "Cadmium", "Mercury", "Selenium", "Tellurium", "Thallium", "Zinc", "Jarosite", "Hematite", "Copper", "cupric chloride", "organohalogen", 
                 "heavy metal", "toxic metal", "acrylamide", "persistent organic pollutant", "POP compounds", 
                 "aldrin", "chlordane", "dieldrin", "heptachlor", "hexachlorobenzen", "mirex", "organochloride",
                 "polychlorinated biphenyls", "polychlorinated dibenzo-p-dioxin", "polychlorinated dibenzofuran", "toxaphen", "neonicotinoid",
                 
                 "kjemikalie", "rengjøringsprodukt", "rengjøringsmid", "desinfeksjonsmid", "motorolje", "mikroplast", "plastpartik", "plastavfall",
                 "insektmid", "plantevernmid", "batteri", "giftig", "maling", 
                 "arsenikk", "kadmium", "kvikksølv", "kobber", "tallium",  
                 "tungmetall", "persistente organiske miljøgift",
                 "tinnorganiske", "organiske tinnforbindelse",
                 "bioakkumuler", "dioksin", "neonikotinoid"]

termlist12_4c_trunc = ["paint", "paints", "Lead", "DDT", "PCB",
                       "bly", "plast", "endrin"]

termlist12_4d = ["Dubai Declaration on International Chemicals Management", "Strategic Approach to International Chemicals Management", "SAICM" ]

termlist12_4not = ["herbicide tolerant" ]
#This is a specific phrase included for the Norwegian searches - there are a number of reports with risk assessments for "herbicide tolerant" GM crops

phrasespecific12_4a = r'\b(?:{})\b'.format('|'.join(termlist12_4a_trunc))
phrasespecific12_4b = r'\b(?:{})\b'.format('|'.join(termlist12_4b_trunc))
phrasedefault12_4b = r'(?:{})'.format('|'.join(termlist12_4b))
phrasedefault12_4c = r'(?:{})'.format('|'.join(termlist12_4c))
phrasespecific12_4c = r'\b(?:{})\b'.format('|'.join(termlist12_4c_trunc))
phrasedefault12_4d = r'(?:{})'.format('|'.join(termlist12_4d))
phrasedefault12_4not = r'(?:{})'.format('|'.join(termlist12_4not))
```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault12_4d, na=False, case=False))
        |
        (
            (
                ((Data['result_title'].str.contains(phrasespecific12_4a, na=False, case=False)) & (Data['result_title'].str.contains(phrasespecific12_4b, na=False, case=False)))
                | (Data['result_title'].str.contains(phrasedefault12_4b, na=False, case=False))
            )
            & ((Data['result_title'].str.contains(phrasedefault12_4c, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific12_4c, na=False, case=False)))
        )
    ) & (~Data['result_title'].str.contains(phrasedefault12_4not, na=False, case=False))
),"tempsdg12_04"] = "SDG12_04"

print("Number of results = ", len(Data[(Data.tempsdg12_04 == "SDG12_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_04 == "SDG12_04"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 2 (& 5)
Note that this will also cover phrase 5 wos string, which uses the terms `"unsustainab*" OR "irresponsib*" OR "unecological*" OR "unsafe"` (covered by truncation here).


```python
#Termlists
# Reuse 4a from above (sustainable OR responsible etc.)

termlist12_4e_trunc = ["life cycle.*", "lifecycle.*",
                       "management", "handling", "packaging", "labelling", "storing", "storage", "stored",
                       "disposal", "dispose", "transport.*", "process.*", "logistics",
                       "incinerat.*", "combust.*", "collect.*", "treatment", "processing", "processed", "sorting", "sorted",
                       
                       "livssyklus.*", "livløp.*", 
                       "håndter.*", "innpakning", "emballasje", "emballering", "stempel", "merking", "akkredit.*", "sertifi.*", "oppbevar.*", "lagring", 
                       "avhend.*", "tømming", "prossess", "forsyningskjede", "logistikk",
                       "innsaml.*", "samling", "behand.*", "prossess.*", "sorter.*", "forbrenning"]
                      
termlist12_4f = ["waste", "garbage", "trash", "litter ", "rubbish", "sewage", "sludge", "street sweepings", "construction debris", "demolition debris",
                 "avfall", "søppel", "kloakk", " slam", "byggrester"]
# The space after "litter " is intentional to stop "litteratur" (NO)

termlist12_4g = ["recycl", "reuse", "re-use", "reusing", "re-using",
                "refurbish", "re-furbish", "remanufactur", "re-manufactur", "repurpos", "re-purpos",
                "compost", "codigest", "co-digest",
                "footprint", "cradle to cradle", "cradle-to-cradle", "end of life", "end of chain", "life cycle analysis", "lifecycle analysis", 
                 
                 "resirkul", "gjenbruk", "ombruk", 
                 "kompost",
                 "forspør", "vugge til vugge", "livssyklusanalyser", "livsløpsanalyser"]

termlist12_4h = ["Basel Convention", "Rotterdam Convention", "Stockholm Convention", "Montreal Protocol", "Minamata Convention", "Bamako Convention",
                 "Baselkonvensjonen", "Rotterdamkonvensjonen", "Stockholmkonvensjonen", "Minamatakonvensjonen", "Bamakokonvensjonen",
                 "Basel-konvensjonen", "Rotterdam-konvensjonen", "Stockholm-konvensjonen", "Minamata-konvensjonen", "Bamako-konvensjonen"]

phrasespecific12_4e = r'\b(?:{})\b'.format('|'.join(termlist12_4e_trunc))
phrasedefault12_4f = r'(?:{})'.format('|'.join(termlist12_4f))
phrasedefault12_4g = r'(?:{})'.format('|'.join(termlist12_4g))
phrasedefault12_4h = r'(?:{})'.format('|'.join(termlist12_4h))
```


```python
#Search
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault12_4f, na=False, case=False))
    &
        (
            (Data['result_title'].str.contains(phrasedefault12_4g, na=False, case=False))
            |((Data['result_title'].str.contains(phrasespecific12_4a, na=False, case=False)) & (Data['result_title'].str.contains(phrasespecific12_4e, na=False, case=False)))
        )
    )
    |(Data['result_title'].str.contains(phrasedefault12_4h, na=False, case=False))
    ),"tempsdg12_04"] = "SDG12_04"

print("Number of results = ", len(Data[(Data.tempsdg12_04 == "SDG12_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_04 == "SDG12_04"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
# Reuse phrasedefault12_4f, phrasedefault12_4c and phrasespecific12_4c from phrases 1 and 2 (wastes and chemicals)

termlist12_4i = ["reduc", "minim", "decreas", "stopping", "avoid", "prevent", "combat", "tackl", "resist", "lowering", "lowered", "prohibit", "cleanup", "clean up",
                 "reduse", "unngå", "hinder", "hindre", "kjempe", "lavere", "forby", "rengjør", "rydde opp"]

termlist12_4i_trunc = ["stop", "end", "ends", "ending", "ended", "halt", "halting", "lower",
                       "stoppe", "avta", "avtar"]
                      
termlist12_4j = ["releas", "emission", "effluent", "discharge", "pollut", "contaminat",
                 "utslipp", "forurens", "forurein", "kontamin"]

phrasedefault12_4i = r'(?:{})'.format('|'.join(termlist12_4i))
phrasespecific12_4i = r'\b(?:{})\b'.format('|'.join(termlist12_4i_trunc))
phrasedefault12_4j = r'(?:{})'.format('|'.join(termlist12_4j))
```


```python
#Search
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault12_4i, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific12_4i, na=False, case=False)))
    & (Data['result_title'].str.contains(phrasedefault12_4j, na=False, case=False))
    & 
    (
        (Data['result_title'].str.contains(phrasedefault12_4c, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasespecific12_4c, na=False, case=False))
        | (Data['result_title'].str.contains(phrasedefault12_4f, na=False, case=False))
    )
    ),"tempsdg12_04"] = "SDG12_04"

print("Number of results = ", len(Data[(Data.tempsdg12_04 == "SDG12_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_04 == "SDG12_04"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 4


```python
#Termlists
# Reuse phrasedefault12_4f, phrasedefault12_4c and phrasespecific12_4c from phrases 1 and 2 (wastes and chemicals)

termlist12_4k = ["reduc", "minim", "decreas", "avoid", "prevent", "combat", "tackl", "resist", "lowering", "lowered", "control", "assess", "evaluat", "monitor",
                 "reduse", "unngå", "hinder", "hindre", "kjempe", "lavere", "forby","kontroll", "vurder", "evaluering", "overvåk"]

termlist12_4k_trunc = ["stop", "stopping", "lower", 
                       "stoppe"]
                      
termlist12_4l = ["health", "wellbeing", "well-being", "risk", "hazard", "danger", "effect",
                 "helse", "risiko", "farlig", "miljøfare", "effekt", "påvirk"]

phrasedefault12_4k = r'(?:{})'.format('|'.join(termlist12_4k))
phrasespecific12_4k = r'\b(?:{})\b'.format('|'.join(termlist12_4k_trunc))
phrasedefault12_4l = r'(?:{})'.format('|'.join(termlist12_4l))
```


```python
#Search
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault12_4k, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific12_4k, na=False, case=False)))
    & (Data['result_title'].str.contains(phrasedefault12_4l, na=False, case=False))
    & 
    (
        (Data['result_title'].str.contains(phrasedefault12_4c, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasespecific12_4c, na=False, case=False))
        | (Data['result_title'].str.contains(phrasedefault12_4f, na=False, case=False))
    )
    ),"tempsdg12_04"] = "SDG12_04"

print("Number of results = ", len(Data[(Data.tempsdg12_04 == "SDG12_04")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_04 == "SDG12_04"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.5

*12.5 By 2030, substantially reduce waste generation through prevention, reduction, recycling and reuse*

*Innen 2030 redusere avfallsmengden betydelig gjennom forebygging, reduksjon, materialgjenvinning og ombruk*


#### Phrase 1


```python
#Termlists

termlist12_5a = ["waste", "sludge", "garbage", "trash", "litter "]
# Waste terms with multiple meanings. The space after "litter " is intentional to stop "litteratur" (NO)

termlist12_5b = ["agrowaste", "solid waste", "bio-waste", "biowaste",
                 "ewaste", "e-waste", "electronic waste",
                 "rubbish", "sewage",  "street sweepings", "construction debris",  
                 
                 "avfall", "søppel", "kloakk", " slam", "byggrester"]
#Waste terms which are generally to do with physical/chemical waste. Most Norwegian terms are covered by "avfall" (e.g. spesialavfall, landbruksavfall) and don't needs specifying.

termlist12_5c = ["household", "domestic", "residential", 
                 "commerce", "commercial", "trade", "business", "office", 
                 "institution", "schools", "hospital", "municipal", "urban", "cities",
                 "industr", "manufacturing", "hotel", "restaurant",
                 
                 "hushold", "domestik", "privat",
                 "kommersiel", "bedrift", "kontor", "byggeplass"
                 "institusjon", "skole", "sykehus", "sjukehus", "kommunal", "byer"]

termlist12_5d = ["generation", "generated",                
                 "generer"]   

termlist12_5e_trunc = ["reduc.*" , "minimi.*" , "decreas.*" , "stop" , "end" , "ends" , "ended" , "ending" , "eliminat.*",
                       "avoid.*" , "prevent.*" , "combat.*" , "tackl.*" , "halt.*" , "resist" , "resisting" , "lowering" , "lower" , "lowered"]

phrasedefault12_5a = r'(?:{})'.format('|'.join(termlist12_5a))
phrasedefault12_5b = r'(?:{})'.format('|'.join(termlist12_5b))
phrasedefault12_5c = r'(?:{})'.format('|'.join(termlist12_5c))
phrasedefault12_5d = r'(?:{})'.format('|'.join(termlist12_5d))
phrasespecific12_5e = r'\b(?:{})\b'.format('|'.join(termlist12_5e_trunc))
```


```python
#Search
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault12_5a, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault12_5b, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault12_5d, na=False, case=False))
    )
    |
    (
        (Data['result_title'].str.contains(phrasespecific12_5e, na=False, case=False))
        & 
            (
                (Data['result_title'].str.contains(phrasedefault12_5b, na=False, case=False))
                |((Data['result_title'].str.contains(phrasedefault12_5a, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_5c, na=False, case=False)))
            )
    )
),"tempsdg12_05"] = "SDG12_05"

print("Number of results = ", len(Data[(Data.tempsdg12_05 == "SDG12_05")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_05 == "SDG12_05"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists

termlist12_5f = ["recycl", "reuse", "re-use", "reusing", "re-using",
                "refurbish", "re-furbish", "remanufactur", "re-manufactur", "repurpos", "re-purpos",
                "compost", "codigest", "co-digest",
                "resource efficien", "resource-use efficien", "material efficicen", "material-use efficien",
                "life cycle", "lifecycle", "footprint", "cradle to cradle", "cradle-to-cradle",
                "cleaner production",
                 
                "resirkul", "gjenbruk", "ombruk",
                "kompost",
                "ressurseffektiv", "materialeffektiv", "effektiv bruk av material", "effektiv bruk av ressurs",
                "livssyklusanalyse", "livsløpsvurdering", "fotspor", "vugge til vugge"]

termlist12_5g = ["sidestream", "side-stream", "byproduct", "by-product",
                "waste", "garbage", "trash", "litter", "rubbish", "sewage", "sludge", "street sweepings", "construction debris",  
                 
                "sidestrøm", "biprodukt",
                "avfall", "søppel", "kloakk", " slam", "byggrester"]

termlist12_5h = ["recycl", "reuse", "re-use", "reusing", "re-using",
                "refurbish", "re-furbish", "remanufactur", "re-manufactur", "repurpos", "re-purpos",
                "compost", "codigest", "co-digest",
                "cradle to cradle", "cradle-to-cradle",
                 
                "resirkul", "gjenbruk", "ombruk",
                "kompost",
                "vugge til vugge"]

termlist12_5i = ["bioeconom", "bio-econom", 
                 "produc", "consum", "packaging", 
                 "resource", "material", "matter", "biomass",
                 
                 "bioøkonomi", "produksj", "forbruk",
                 "innpakning", "emballasje", "emballering", 
                 "ressurs"]

termlist12_5j = ["circular econom", "circular bioeconom", "circular product", "circular consumption", "zero waste",
                 "sirkulær økonomi", "sirkulær bioøkonomi", "sirkulær produk", "sirkulær forbruk", "null avfall", "null svinn"]

termlist12_scp4_trunc = ["utili.*", "use", "usage", "design.*",
                         "bruk.*", "forbruk"]
termlist12_scp5 = ["sidestream", "side-stream", "byproduct", "by-product",
                   "sidestrøm", "biprodukt"]

termlist12_scp2_trunc = ["green", "eco", "sustainab.*", "responsib.*", "environmental.*", "ecological.*",
                         "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "ansvarlig.*", "miljø.*"]

termlist12_5k = ["footprint", "lifecycle analys", "lifecycle assess", "material lifecycle", "cradle to cradle", "cradle-to-cradle",
                 "livssyklusanalyse", "livsløpsvurdering", "fotspor", "vugge til vugge"]

termlist12_5l = ["recycl", "reuse",                 
                "resirkul", "gjenbruk"]
                                        
phrasedefault12_5f = r'(?:{})'.format('|'.join(termlist12_5f))
phrasedefault12_5g = r'(?:{})'.format('|'.join(termlist12_5g))
phrasedefault12_5h = r'(?:{})'.format('|'.join(termlist12_5h))
phrasedefault12_5i = r'(?:{})'.format('|'.join(termlist12_5i))
phrasedefault12_5j = r'(?:{})'.format('|'.join(termlist12_5j))
phrasespecific12_scp4 = r'\b(?:{})\b'.format('|'.join(termlist12_scp4_trunc))
phrasedefault12_scp5 = r'(?:{})'.format('|'.join(termlist12_scp5))
phrasespecific12_scp2 = r'\b(?:{})\b'.format('|'.join(termlist12_scp2_trunc))
phrasedefault12_5k = r'(?:{})'.format('|'.join(termlist12_5k))
phrasedefault12_5l = r'(?:{})'.format('|'.join(termlist12_5l))
```


```python
#Search
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault12_5f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_5g, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasedefault12_5h, na=False, case=False)) &  (Data['result_title'].str.contains(phrasedefault12_5i, na=False, case=False)))
    | (Data['result_title'].str.contains(phrasedefault12_5j, na=False, case=False))
    | ((Data['result_title'].str.contains(phrasespecific12_scp4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_scp5, na=False, case=False)))
    | 
    (
        (Data['result_title'].str.contains(phrasespecific12_scp2, na=False, case=False)) 
        & 
            (
                (Data['result_title'].str.contains(phrasedefault12_5k, na=False, case=False))
                |(Data['result_title'].str.contains(phrasedefault12_5l, na=False, case=False))
            )
    )
    ),"tempsdg12_05"] = "SDG12_05"

print("Number of results = ", len(Data[(Data.tempsdg12_05 == "SDG12_05")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_05 == "SDG12_05"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.6

*12.6 Encourage companies, especially large and transnational companies, to adopt sustainable practices and to integrate sustainability information into their reporting cycle*

*Stimulere selskaper, særlig store og flernasjonale selskaper, til å ta i bruk bærekraftige metoder og integrere informasjon om egen  bærekraft i sine rapporteringsrutiner*


#### Phrase 1


```python
#Termlists

#Here we use the whole scp phrase, and supplement with 6a + scp2

termlist12_scp2_trunc = ["green", "eco", "sustainab.*", "responsib.*", "environmental.*", "ecological.*",
                         "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "ansvarlig.*", "miljø.*"]

termlist12_6a = ["practic", "procedure", "custom", "culture", "praxis", "method", "policy", "policies", "standard", "code of conduct",
                 "praksis", "kultur", "metoder", "politikk", "retningslinje"]

termlist12_6c = ["company", "companies", "organisation", "organization", "corporation", "conglomerate", "business", "corporate",
                 "producer", "industry", "industries", "industrial sector", "manufacturer", "manufacturing sector", "commercial sector",
                 "institution",
                 
                 "bedrift", "kontor", "organisasjon", "selskap", "konglomerat",
                 "industrier", "industrien", "industri ", "industrisektor", "produsent", "produksjonssektor", "kommersiell sektor", "kommersielle sektor", 
                 "institusjon"] 
termlist12_6c_trunc = ["firms", "firm"] 
# "Industri" (NO) has a space after to prevent "industriasliert" but allow e.g. "kjemikalieindustri"

phrasespecific12_scp2 = r'\b(?:{})\b'.format('|'.join(termlist12_scp2_trunc))
phrasedefault12_6a = r'(?:{})'.format('|'.join(termlist12_6a))
phrasedefault12_6c = r'(?:{})'.format('|'.join(termlist12_6c))
phrasespecific12_6c = r'\b(?:{})\b'.format('|'.join(termlist12_6c_trunc))
```


```python
#Search
Data.loc[(
    (
        (Data['scp']==True)
        |((Data['result_title'].str.contains(phrasespecific12_scp2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_6a, na=False, case=False)))
    )
    & ((Data['result_title'].str.contains(phrasedefault12_6c, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific12_6c, na=False, case=False)))
    ),"tempsdg12_06"] = "SDG12_06"

print("Number of results = ", len(Data[(Data.tempsdg12_06 == "SDG12_06")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_06 == "SDG12_06"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
# Reuse lists phrasespecific12_6c and phrasedefault12_6c from phrase 1 for companies terms

termlist12_6d = ["sustainab", "responsib", "environmental",
                "bærekraft", "berekraft", "ansvarlig", "miljøvurder", "miljøprestasjon", "miljøstyring", "miljøsertifiser", "miljøinformasjon"]
#"environmental" works ok alone in English, but in Norwegian (miljø) creates some noise. 

termlist12_6e = ["report", "accounting", "publish", "disclos",
                 "rapport", "regnskap", "publiser", "avslør", "offentliggjør", "offentleggj"]

termlist12_6f = ["environmental information disclos"]

phrasedefault12_6d = r'(?:{})'.format('|'.join(termlist12_6d))
phrasedefault12_6e = r'(?:{})'.format('|'.join(termlist12_6e))
phrasedefault12_6f = r'(?:{})'.format('|'.join(termlist12_6f))
```


```python
#Search
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault12_6d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_6e, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault12_6f, na=False, case=False))
    )
    & ((Data['result_title'].str.contains(phrasedefault12_6c, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific12_6c, na=False, case=False)))
    ),"tempsdg12_06"] = "SDG12_06"

print("Number of results = ", len(Data[(Data.tempsdg12_06 == "SDG12_06")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_06 == "SDG12_06"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.7

*12.7 Promote public procurement practices that are sustainable, in accordance with national policies and priorities*

*Fremme bærekraftige ordninger for offentlige anskaffelser, i samsvar med de enkelte landenes politikk og prioriteringer*



```python
#Termlists

#termlist12_7a = ["sustainable public procurement", "circular public procurement", "green public procurement",
#                 "bærekraftige offentlige anskaffelse", "bærekraftig offentlig anskaffelse", "bærekraftige anskaffelse", "bærekraftig anskaffelse", "bærekraftig fellesavtale", "bærekraftige fellesavtale",
#                 "berekraftige offentlige anskaffelse", "berekraftig offentlig anskaffelse", "berekraftige anskaffelse", "berekraftig anskaffelse", "berekraftig fellesavtale", "berekraftige fellesavtale", 
#                ]
#Not needed

termlist12_scp2_trunc = ["green", "eco", "eco-.*", "sustainab.*", "responsib.*", "environmental.*", "ecological.*", "circular",
                         "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "ansvarlig.*", "miljø.*", "sirkulær"]

termlist12_7b = ["fair trade", "human rights",
                 "lifecycle", "life cycle", 
                 "employment of minorities", "employment of minority",
                 "Best value for Money", "Most Economically Advantageous Tender",
                 
                 "rettferdig handel", "menneskerettigheter",
                 "livssyklus", "livsløps",
                 "likestilt rekruttering", "ansette minoriteter", "ansette etniske minoriteter",
                 "økonomisk mest fordelaktige"]

termlist12_7c = ["procurement", "aquisition", "purchas", "contract", "tender",
                 "anskaffels", "anbud", "innkjøp", "kontrakt", "tilbudet"] 

#termlist12_7d = ["national", "countr", "domestic", "government", "administrat", "public", "authorit"] 
#We have not included 7d in the final search as it lost relevant results in a title search. A few less relevant creep in (about e.g. consumer purchasing), but more relevant are lost.

#phrasedefault12_7a = r'(?:{})'.format('|'.join(termlist12_7a))
phrasespecific12_scp2 = r'\b(?:{})\b'.format('|'.join(termlist12_scp2_trunc))
phrasedefault12_7b = r'(?:{})'.format('|'.join(termlist12_7b))
phrasedefault12_7c = r'(?:{})'.format('|'.join(termlist12_7c))
#phrasedefault12_7d = r'(?:{})'.format('|'.join(termlist12_7d))
```


```python
#Search
Data.loc[(
    #(Data['result_title'].str.contains(phrasedefault12_7a, na=False, case=False))
    #|
    (
        ((Data['result_title'].str.contains(phrasespecific12_scp2, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault12_7b, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault12_7c, na=False, case=False))
        #& (Data['result_title'].str.contains(phrasedefault12_7d, na=False, case=False))
    )
    ),"tempsdg12_07"] = "SDG12_07"

print("Number of results = ", len(Data[(Data.tempsdg12_07 == "SDG12_07")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_07 == "SDG12_07"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.8

*12.8 By 2030, ensure that people everywhere have the relevant information and awareness for sustainable development and lifestyles in harmony with nature*

*Innen 2030 sikre at alle mennesker i hele verden har relevant informasjon om og forståelse av bærekraftig utvikling og et levesett som er i harmoni med naturen*


#### Phrase 1 & 2


```python
#Termlists

termlist12_8a = ["education for sustainable", "education in sustainable", "sustainable development educat", "sustainability educat", 
                 "utdanning for bærekraft", "utdanning for berekraft", "bærekraftig utvikling utdann", "berekraftig utvikling utdann"]

termlist12_8b = ["awareness", "lifelong learn", "life-long learn",
                 "oppmerksom", "bevisst", "livslang læring"]

termlist12_8c = ["inform", "knowledge", "aware", "educat", "guide", "instruct", "learn", "educat", "teach",
                 "kunnskap", "kjennskap", "kjenne", "veiled", "undervis", "læring", "lære", "utdann", "kompetans", "engasj"] 

termlist12_8g = ["consumer", "customer", "resident", "visitor", "guest", "tourist", "employee", "farmer",
                 "citizen", "children", "teenager", "adolescent", "the elderly", "public", "student", "adult",
                 "purchas", "buying", "habit",
                 "consumption", "lifestyle", "life-style",
                 
                 "forbruk", "beboer", "bebuar", "besøkende", "besøkande", "gjest", "turist", "ansatt", "bonde",
                 "borger", "folk", "barna", "barne", "tenåring", "de gamle", "offentlig", "voksne", "voksen", "vaksne", "vaksen",
                 "kjøp", "vane"
                 "livstil"] 

termlist12_8d_trunc = ["green", "eco", "eco-.*", "sustainab.*", "environmental.*", "ecological.*", "social responsib", "socially responsib", "circular",
                       "cleaner production",
                       "resource efficien.*", "resource use efficiency" , "material efficiency" , "material use efficiency" , "energy efficiency",
                       "eco-label.*", "ecolabel.*", "environmental label.*",
                       "ecotouris.*", "eco-touris.*",
                       "ecobuilding.*", "eco-building.*", "eco-housing", "eco-construct.*", "eco-design", "eco-technolog.*",
                       "footprint", "cradle-to-cradle", "cradle to cradle",
                       "recycl", "reuse", "re-use", "reusing", "re-using", "refurbish.*", "re-furbish.*", "remanufactur.*", "re-manufactur.*", "repurpos.*", "re-purpos.*", "compost.*",
                       "renewable energy",
                       
                       "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "miljø.*", "sosial ansvar.*", "sosialt ansvar.*", "sirkulær.*",
                       "renere produksjon.*",
                       "ressurseffektiv.*", "materialeffektiv.*", "effektiv bruk av material", "effektiv bruk av ressurs.*", 
                       "miljømerk.*", "svanemerk.*",
                       "økoturism",
                       "fotspor", "vugge til vugge",
                       "resirkul", "gjenbruk", "ombruk", "kompost",
                       "fornybar energi"] 

termlist12_8e = ["responsible",
                "ansvarlig", "ansvarleg"]

termlist12_8f_trunc = ["consumer.*", "consumption", "tourism", "product", "lifestyle.*", "life-style.*", "purchas.*", "waste",
                       "forbruk.*", "turist.*", "turism", "produksj.*", "produkt.*", "livstil.*", "kjøp", "avfall"]

phrasedefault12_8a = r'(?:{})'.format('|'.join(termlist12_8a))
phrasedefault12_8b = r'(?:{})'.format('|'.join(termlist12_8b))
phrasedefault12_8c = r'(?:{})'.format('|'.join(termlist12_8c))
phrasespecific12_8d = r'\b(?:{})\b'.format('|'.join(termlist12_8d_trunc))
phrasedefault12_8e = r'(?:{})'.format('|'.join(termlist12_8e))
phrasespecific12_8f = r'\b(?:{})\b'.format('|'.join(termlist12_8f_trunc))
phrasedefault12_8g = r'(?:{})'.format('|'.join(termlist12_8g))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault12_8a, na=False, case=False))
    |
    (
        ((Data['result_title'].str.contains(phrasedefault12_8b, na=False, case=False)) 
         | ((Data['result_title'].str.contains(phrasedefault12_8c, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_8g, na=False, case=False)))
        )
        & 
        (
            (Data['result_title'].str.contains(phrasespecific12_8d, na=False, case=False))
            |((Data['result_title'].str.contains(phrasedefault12_8e, na=False, case=False)) & (Data['result_title'].str.contains(phrasespecific12_8f, na=False, case=False)))
        )
    )
    ),"tempsdg12_08"] = "SDG12_08"

print("Number of results = ", len(Data[(Data.tempsdg12_08 == "SDG12_08")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_08 == "SDG12_08"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.a

*12.a Support developing countries to strengthen their scientific and technological capacity to move towards more sustainable patterns of consumption and production*

*Støtte utviklingslandene i å styrke deres vitenskapelige og tekniske kapasitet til å innføre mer bærekraftige forbruks- og produksjonsmønstre*


#### Phrase 1


```python
#Termlists
# Using the scp and country strings already created
#Some terms are simplified for a title search - e.g. "managerial support" -> Support; "financial resources" -> financ; "institional capacity" -> capacity

termlist12_a1 = ["capacity", "support", "resources"
                 "infrastructure", "facilities", "tools", 
                 "research", "scientific", "knowledge", "skills", "competenc", "expertise", "R&D", "innovation", "technolog", "cleantech",
                 "communication", "social network", "information network", "campaign", 
                 "awareness", "disseminat", "educat", "training",
                 "cooperation", "collaboration", "partnership", 
                 "transfer of technolog", "technological transfer", "technology transfer",               
                 "expenditure", "investing", "investment", "financ", "spending", "funding", "funder", 
                 "incentive", "subsidy", "subsidies", "subsidis", "subsidiz", 
                 "development spending", "development aid", "development assistance", "foreign aid", "foreign assistance", "international aid", "international assistance", 
                 "policy", "policies", "empower", "strateg", "program", "intervention", 
                 
                 "kapasitet", "hjelp", "bistand", "støtte", "stønad", "ressurs",
                 "infrastruktur", "fasilitet", "verktøy",
                 "forskning", "vitenskapelig", "kunnskap", "ferdighet", "kompetans", "ekspertis", "innovasjon", "teknologi",
                 "kommunikasjon", "sosiale nettverk", "informasjonsnettverk", "kampanje",
                 "bevisst", "utdanning", "opplær" 
                 "samarbeid", "felles", "partner", 
                 "teknologioverføring", "overfører teknologi", "overføre teknologi",
                 "utgift", "invester", "finans", "pengebruk", "kapital",
                 "insentiv", "subsider", 
                 "bistand", "utviklingssamarbeid", "utviklingsstøtte", "utviklingsstønad", "utviklingshjelp", "u-hjelp", "samarbeidsfond",
                 "politikk", "retningslin", "myndiggjør", "strategi", "intervensjon"]

termlist12_a1_trunc = ["invest", "fund", "funds", "grant", "grants", "tax", "taxes", "fees", "ODA",
                      "fond", "bevilgning", "midler", "skatt", "skatter", "FoU"]

phrasedefault12_a1 = r'(?:{})'.format('|'.join(termlist12_a1))
phrasespecific12_a1 = r'\b(?:{})\b'.format('|'.join(termlist12_a1_trunc))
```


```python
#Search
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault12_a1, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific12_a1, na=False, case=False)))
    & (Data['scp']==True)
    & (Data["LMICs"]==True)
    ),"tempsdg12_a"] = "SDG12_0a"

print("Number of results = ", len(Data[(Data.tempsdg12_a == "SDG12_0a")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_a == "SDG12_0a"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
# Using the country strings already created, and the capacity string from phrase 1

termlist12_a2 = ["energy transition",  
                 "geothermal heat pump", "ground source heat pump", 
                 "solar PV", "photovoltaic", "solar cell", "solar-cell", "solar panel", "solar-panel", "solar array", "solar energy collector", "solar farm", "solar plant", "solar park", 
                 "solar district heating", "solar district cooling", "solar air heating system", "solar space heating system", 
                 "wind farm", "wind turbine", "wind park", "wind factory", "wind factories", 
                 "hydropower", "hydroelectric", "hydro-electric", "tidal turbine", "stream turbine", "current turbine", "tidal power", "tidal energy", "marine energy", "wave energy", 
                 
                 "energiomstilling", 
                 "geotermisk varmepump", 
                 "solcelle", "solkraft", "solenergi", "fotovoltaisk", "solfang", "solsaml", "solvarm", "solpark", "solcellepark",
                 "vindkraftverk", "vindturbin", "vindpark", "vindmøllepark", "havvind", "vindenergi",
                 "vannkraft", "vasskraft", "hydroelektrisk", "tidevannsturbin", "havstrømturbin", "tidevannskraft", "tidevannsenergi", "bølgeenergi", "marin energi", "havenergi"]

termlist12_a3 = ["power", "energy", "electricity",
                 "kraft", "energi", "elektrisit"]
                 
termlist12_a4 = ["clean", "sustainab", "renewable",
                 "solar", "thermal energy", "wind",
                 "geothermal", "hydrothermal", 
                 "hydrokinetic", "marine", "tidal", "wave energy", "ocean energy",
                 "bioenergy", "biofuel", "biodiesel",
                                 
                 "ren energi", "bærekraftig", "berekraftig", "fornybar",
                 "solcelle", "solkraft", "solenergi", "fotovoltaisk", "solfang", "solsaml", "solvarm", "solpark", "solcellepark",
                 "geotermisk",
                 "bioenergi", "biodrivstoff"]

phrasedefault12_a2 = r'(?:{})'.format('|'.join(termlist12_a2))
phrasedefault12_a3 = r'(?:{})'.format('|'.join(termlist12_a3))
phrasedefault12_a4 = r'(?:{})'.format('|'.join(termlist12_a4))
```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault12_a1, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific12_a1, na=False, case=False))
    )
    & 
    (
        (Data['result_title'].str.contains(phrasedefault12_a2, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault12_a3, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_a4, na=False, case=False)))
    )
    & (Data["LMICs"]==True)
    ),"tempsdg12_a"] = "SDG12_0a"

print("Number of results = ", len(Data[(Data.tempsdg12_a == "SDG12_0a")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_a == "SDG12_0a"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.b

*12.b Develop and implement tools to monitor sustainable development impacts for sustainable tourism that creates jobs and promotes local culture and products*

*Utvikle og innføre metoder for å måle effekten av bærekraftig reiseliv som skaper arbeidsplasser og fremmer lokal kultur og lokale produkter*



```python
#Termlists
#Simplified to remove the "effect" terms - not really needed 

termlist12_b1 = ["monitor", "report", "account", "control", "measur", "assess", "evaluat", "survey",
                 "overvåk", "rapport", "styring", "forvalt", "måling", "evaluer", "vurder", "undersøke"]

termlist12_scp2_trunc = ["green", "eco", "eco-.*", "sustainab.*", "responsib.*", "environmental.*", "ecological.*",
                        "grønne.*", "grønn", "øko", "bærekraft.*", "berekraft.*", "ansvarlig.*", "miljø.*"]

termlist12_b2 = ["tourism", "tourist", "hospitality", "leisure", "air travel", "hotel",
                 "turism", "turist", " reise", "fritid", "flyreise", "syden"]

termlist12_b3 = ["ecotourism", 
                 "økoturism"]

phrasedefault12_b1 = r'(?:{})'.format('|'.join(termlist12_b1))
phrasespecific12_scp2 = r'\b(?:{})\b'.format('|'.join(termlist12_scp2_trunc))
phrasedefault12_b2 = r'(?:{})'.format('|'.join(termlist12_b2))
phrasedefault12_b3 = r'(?:{})'.format('|'.join(termlist12_b3))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault12_b1, na=False, case=False))
    &
    (
        (Data['result_title'].str.contains(phrasedefault12_b3, na=False, case=False))
        |((Data['result_title'].str.contains(phrasespecific12_scp2, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault12_b2, na=False, case=False)))
    )
    ),"tempsdg12_b"] = "SDG12_b"

print("Number of results = ", len(Data[(Data.tempsdg12_b == "SDG12_b")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_b == "SDG12_b"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12.c

*12.c Rationalize inefficient fossil-fuel subsidies that encourage wasteful consumption by removing market distortions, in accordance with national circumstances, including by restructuring taxation and phasing out those harmful subsidies, where they exist, to reflect their environmental impacts, taking fully into account the specific needs and conditions of developing countries and minimizing the possible adverse impacts on their development in a manner that protects the poor and the affected communities*

*Redusere ineffektive subsidier til fossilt brensel ved å fjerne markedsvridninger som oppmuntrer til overforbruk, i samsvar med nasjonale forhold, blant annet ved å legge om skatter og avgifter og avvikle skadelige subsidier der de finnes, slik at konsekvensene for miljøet avdekkes, og samtidig fullt ut ta hensyn til utviklingslandenes særlige behov og situasjon og begrense eventuelle negative konsekvenser for deres utvikling mest mulig og på en måte som beskytter de fattige og de berørte lokalsamfunnene*


#### Phrase 1


```python
#Termlists
termlist12_c2 = ["subsidi", "subsidy", "fiscal incentive", "price support", "underpricing", "underprice", "under-pricing", "under-price", "under pricing", "under price", 
                 "below market lending", "below market loan", "below-market",
                 "credit support", "credit guarantee", "credit restructur", "credit cancel", 
                 "loan support", "loan guarantee", "loan restructur", "loan cancel", 
                 "debt support", "debt guarantee", "debt restructur", "debt cancel", 
                 "market distor", "price distortion",
                 "government spending", "government funding", "government ownership", "government payment",
                 
                 "næringsstøtte", "insentiv", "prisstøtte", "prisstønad", "økonomisk støtte", "økonomisk stønad", "tilskudd", "tilskot", "prissetting",
                 "kreditt", " lån", "gjeld",
                 "vridning",
                 "offentlige utgifter", "statlig eier", "offentlig forvalt", "statlig forvalt", "finansiell støtte", "finansiell stønad", "finansielle ressurs"]

termlist12_c3 = ["fossil fuel", "natural gas", "diesel", "gasoline", "kerosene", "petroleum", "energy resource", "conventional energy",
                 "fossilt brensel", "fossile brensl", "fossilt brennstoff", "fossile brennstoff", "naturgass", "energiressurs", "konvensjonell energi"]

termlist12_c3_trunc = ["coal", "oil", "peat",
                       "kull", "kol", "olje", "torv"]

phrasedefault12_c2 = r'(?:{})'.format('|'.join(termlist12_c2))
phrasedefault12_c3 = r'(?:{})'.format('|'.join(termlist12_c3))
phrasespecific12_c3 = r'\b(?:{})\b'.format('|'.join(termlist12_c3_trunc))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault12_c2, na=False, case=False))
    & ((Data['result_title'].str.contains(phrasedefault12_c3, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific12_c3, na=False, case=False)))
    ),"tempsdg12_c"] = "SDG12_c"

print("Number of results = ", len(Data[(Data.tempsdg12_c == "SDG12_c")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_c == "SDG12_c"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
#reuse fossil fuels from phrase 1

termlist12_c5_trunc = ["taxation", "tax", "taxes", "tariff.*", "duty", "duties", "fees", "fee",
                       ".*skatt.*", ".*avgift.*", "gebyr.*"]

termlist12_c6 = ["heavy duty", "light duty", "medium duty"]

phrasespecific12_c5 = r'\b(?:{})\b'.format('|'.join(termlist12_c5_trunc))
phrasedefault12_c6 = r'(?:{})'.format('|'.join(termlist12_c6))
```


```python
#Search
Data.loc[(
    (Data['result_title'].str.contains(phrasespecific12_c5, na=False, case=False))
    & ((Data['result_title'].str.contains(phrasedefault12_c3, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific12_c3, na=False, case=False)))
    & (~Data['result_title'].str.contains(phrasedefault12_c6, na=False, case=False))
    ),"tempsdg12_c"] = "SDG12_c"

print("Number of results = ", len(Data[(Data.tempsdg12_c == "SDG12_c")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg12_c == "SDG12_c"), ("result_id", "subcategory", "result_title", "SDG_action", "mentionssdgno")]
test.iloc[0:5, ]
```

### SDG 12 mentions

Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 


```python
#Termlists
termlist12_1 = ["SDG 12", "SDGs 12", "SDG12", "sustainable development goal 12", 
               "bærekraftsmål 12", "berekraftsmål 12"]
termlist12_2 = ["sustainable development goal", 
               "bærekraftsmål", "berekraftsmål"]
termlist12_3 = ["goal 12", "mål 12"]
termlist12_4 = ["sustainable development goal", "SDG", "goal 12", 
               "bærekraftsmål", "berekraftsmål", "mål 12"]
termlist12_5 = ["sustainable consumption", "responsible consumption",
               "bærekraftig forbruk", "berekraftig forbruk", "ansvarlig forbruk", "ansvarleg forbruk"]
#Possible search for the short titles of the SDGs, to be used in a title search

phrasedefault12_1 = r'(?:{})'.format('|'.join(termlist12_1))
phrasedefault12_2 = r'(?:{})'.format('|'.join(termlist12_2))
phrasedefault12_3 = r'(?:{})'.format('|'.join(termlist12_3))
phrasedefault12_4 = r'(?:{})'.format('|'.join(termlist12_4))
phrasedefault12_5 = r'(?:{})'.format('|'.join(termlist12_5))
```


```python
#search
Data.loc[(
      (Data['result_title'].str.contains(phrasedefault12_1, na=False, case=False))
      |((Data['result_title'].str.contains(phrasedefault12_2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_3, na=False, case=False)))
      |((Data['result_title'].str.contains(phrasedefault12_4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault12_5, na=False, case=False)))
),"tempmentionsdg12"] = "SDG12"

print("Number of results = ", len(Data[(Data.tempmentionsdg12 == "SDG12")]))
```


```python
test=Data.loc[(Data.tempmentionsdg12 == "SDG12"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 13

### SDG 13.1
13.1 Strengthen resilience and adaptive capacity to climate-related hazards and natural disasters in all countries

Styrkje evna til å stå imot og tilpasse seg til klimarelaterte farar og naturkatastrofar i alle land



```python
#Term lists
termlist13_1a = ["coping", "cope", "adapt", "resilien", "mitigat", "risk reduction", "preparedness", "preparing", "preparation",
                 
                 "takl", "klare", "greie", "holde ut", "halde ut", "tåle", "tole", "utstå", "overkomme", "tilpas", "robust",
                 "mink", "demp", "reduser", "reduksjon", "beredskap", "forbered", "førebu" ]

termlist13_1b = ["mitigat", "prevent", "reduc", "decreas", "minimis", "minimiz", "manag",
                 "mink", "demp", "forebygg", "førebygg", "reduser", "reduksjon", "minimer"]
termlist13_1c = ["impact", "vulnerab",
                 "innflytelse", "innvirkning", "innverknad", "påvirk", "påverk", "betydning", "sårbar"]

termlist13_1d = ["disaster", "risk",
                 "katastrof", "risiko"]
termlist13_1e = ["plan", "assess", "strateg", "program", "policy", "policies", "governance", "reduc", "manag", "medical response", "relief",
                 "vurder", "politikk", "retningslin", "styring", "ledelse", "leiing", "reduser", "reduksjon", "medisinsk", "bistand", "støtte", "stønad"]

termlist13_1f = ["sendai", "cancun", "readiness and preparatory support programme", "readiness programme",
                 "beredskap"]

termlist13_1g = ["extreme",
                 "ekstrem"]
termlist13_1h = ["climat", "weather", "precipitation", "rain", "snow", "temperatur", "storm", "wind",
                 "klima", "vær", "ver", "nedbør", "regn", "snø", "vind"]

termlist13_1i = ["natural", "climat",
                 "naturlig", "naturleg", "klima"]
termlist13_1j = ["hazard", "catastroph", "disaster",
                 "fare", "risiko", "katastrof"]

termlist13_1k = ["rogue wave", "tsunami", "cyclone", "typhoon", "hurricane", "tornado",
                 "drought", "flood",
                 "avalanche", "landslide", "land-slide", "land slide", "rockslide", "rock-slide", "rock slide", "rockfall", "surface collapse", "mudflow", "mud-flow",
                 "cold spell", "cold wave", "dzud", "blizzard", "snowstorm",
                 "heatwave", "heat-wave",
                 "earthquake", "volcan", "ash cloud", "ash fall", "tephra",
                 "wildfire", "wild-fire", "wild fire", "forest-fire", "forest fire", "forestfire",
                 "sea-level rise", "sea-level change", "rising sea-level",

                 "tropisk lavtrykk", "tropisk lågtrykk", "flodbølg", "monsterbølg", "ekstrembølg",
                 "orkan",  "tyfon", "syklon", "snøstorm",
                 "flom", "flaum", "oversvøm", "ovefløym", "tørke",
                 "snøskred", "skred", "snøras", "lavine", "jordskred", "jordras", "sørpeskred", "leirras", "leirskred", "steinras", "steinskred", "synkehull",
                 "uvanlig kulde", "uvanlig kaldt", "uvanleg kulde", "uvanleg kaldt", "ekstrem kuld", "ekstremkuld", "kuldebølg", "snøstorm",
                 "varmebølg", "hetebølg", "ekstrem varm", "ekstremvarm", "uvanlig varm", "uvanleg varm",
                 "jordskjelv", "vulkan", "askenedfall", "oskenedfall", "askesky", "oskesky",
                 "skogbrann", "gressbrann", "grasbrann", "lyngbrann",
                 "havnivåstigning", "stormflo"]

termlist13_1l = ["sea level",
                 "havflate", "havnivå"]
termlist13_1m = ["chang", "rise", "rising",
                 "forandr", "endr", "stig", "øk", "auke", "auking", "hev"]

phrasedefault13_1a = r'(?:{})'.format('|'.join(termlist13_1a))
phrasedefault13_1b = r'(?:{})'.format('|'.join(termlist13_1b))
phrasedefault13_1c = r'(?:{})'.format('|'.join(termlist13_1c))
phrasedefault13_1d = r'(?:{})'.format('|'.join(termlist13_1d))
phrasedefault13_1e = r'(?:{})'.format('|'.join(termlist13_1e))
phrasedefault13_1f = r'(?:{})'.format('|'.join(termlist13_1f))
phrasedefault13_1g = r'(?:{})'.format('|'.join(termlist13_1g))
phrasedefault13_1h = r'(?:{})'.format('|'.join(termlist13_1h))
phrasedefault13_1i = r'(?:{})'.format('|'.join(termlist13_1i))
phrasedefault13_1j = r'(?:{})'.format('|'.join(termlist13_1j))
phrasedefault13_1k = r'(?:{})'.format('|'.join(termlist13_1k))
phrasedefault13_1l = r'(?:{})'.format('|'.join(termlist13_1l))
phrasedefault13_1m = r'(?:{})'.format('|'.join(termlist13_1m))
```


```python
#Search 13_1abcdefghijklm
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault13_1a, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault13_1b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_1c, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault13_1d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_1e, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault13_1f, na=False, case=False))
    )
    &
    (
        ((Data['result_title'].str.contains(phrasedefault13_1g, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_1h, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault13_1i, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_1j, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault13_1k, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault13_1l, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_1m, na=False, case=False)))
    )
),"tempsdg13_01"] = "SDG13_01"

print("Number of results = ", len(Data[(Data.tempsdg13_01 == "SDG13_01")])) 
```


```python
test=Data.loc[(Data.tempsdg13_01 == "SDG13_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13.2
13.2 Integrate climate change measures into national policies, strategies and planning

Innarbeide tiltak mot klimaendringar i politikk, strategiar og planlegging på nasjonalt nivå

#### Phrase 1


```python
# Term lists
termlist13_2a = ["climate change", "global warming", "climatic change", "changing climate", "climate measures", "climate action", "climate adaptation", "climate mitigation", "climate resilience",
                 "klimaendring", "global oppvarming", "klima i endring", "klimamål", "klimahandling", "klimatilpas", "klimaforandring", "klimavariasjon", "klimatiltak"]

termlist13_2b = ["warming",
                 "oppvarming"]
termlist13_2j = ["climat", "atmospher", "ocean",
                 "klima", "atmosfær", "hav"]

termlist13_2k = ["GHG", "greenhouse gas", "carbon footprint", "CO2 footprint", "carbon emission", "CO2 emission", "methane", "ch4", "nitrous oxide", "nox", "n20", "carbon dioxide",
                 "co2", "hydrofluorocarbons", "hfcs", "perfluorocarbons", "pfcs", "sulphur hexafluoride", "sulfur hexafluoride", "sf6",
                 
                 "klimagass", "karbonfotavtrykk", "karbonavtrykk", "karbondioksid", "karbonutslipp", "karbonutslepp", "co2-utslipp", "co2-utslepp", "metan", "dinitrogenoksid", "lystgass",
                 "hydrofluorkarbon", "perfluorkarbon", "svovelheksafluorid"]

termlist13_2l = ["national", "state", "federal", "domestic", "sectoral", "multi level", "multilevel",
                 "nasjonal", "stat", "føderal", "delstat", "fylke", "innenlands", "innalands", "innanlands", "sektor", "kommun"]

termlist13_2m = ["program", "strategy", "framework", "initiativ", "plan", "policy", "policies", "law", "legislat", "governance", "mandat",
                 "nationally determined contribution", "adaptation communication", "monitoring and evaluation", "adaptation committee",
                 
                 "strategi", "rammeverk", "avtale", "overenskomst", "politikk", "retningslin", "lov", "lovgiv", "styring", "ledelse", "leiing",
                 "nasjonalt fastsatt bidrag", "nasjonalt fastsatte bidrag", "nasjonalt fastsette bidrag", "tilpasningskommunikasjon", "tilpassingskommunikasjon", "komite"]

termlist13_2n = ["climate", "global warming", "climatic change",
                 "klima", "global oppvarming"]
termlist13_2o = ["warming",
                 "oppvarming"]
termlist13_2p = ["atmosphere", "ocean",
                 "atmosfære", "hav"]
termlist13_2q = ["GHG", "greenhouse gas", "carbon footprint", "CO2 footprint", "carbon emission", "CO2 emission", "sea-level rise",
                 "drivhusgass", "klimagass", "karbonfotavtrykk", "karbonavtrykk", "karbondioksid", "co2-utslipp", "co2-utslepp", "havnivåstigning"]                                             

phrasedefault13_2a = r'(?:{})'.format('|'.join(termlist13_2a)) 
phrasedefault13_2b = r'(?:{})'.format('|'.join(termlist13_2b))
phrasedefault13_2j = r'(?:{})'.format('|'.join(termlist13_2j)) 
phrasedefault13_2k = r'(?:{})'.format('|'.join(termlist13_2k))
phrasedefault13_2l = r'(?:{})'.format('|'.join(termlist13_2l)) 
phrasedefault13_2m = r'(?:{})'.format('|'.join(termlist13_2m))
phrasedefault13_2n = r'(?:{})'.format('|'.join(termlist13_2n)) 
phrasedefault13_2o = r'(?:{})'.format('|'.join(termlist13_2o))
phrasedefault13_2p = r'(?:{})'.format('|'.join(termlist13_2p)) 
phrasedefault13_2q = r'(?:{})'.format('|'.join(termlist13_2q))
```


```python
#Search 13_2abjklmnopq
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault13_2a, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault13_2b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_2j, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault13_2k, na=False, case=False))   
    )
    & ((Data['result_title'].str.contains(phrasedefault13_2l, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault13_2m, na=False, case=False)))
    &
    (
        (Data['result_title'].str.contains(phrasedefault13_2n, na=False, case=False)) 
        |((Data['result_title'].str.contains(phrasedefault13_2o, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_2p, na=False, case=False))) 
        |(Data['result_title'].str.contains(phrasedefault13_2q, na=False, case=False))
    )   
),"tempsdg13_02"] = "SDG13_02"

print("Number of results = ", len(Data[(Data.tempsdg13_02 == "SDG13_02")]))  
```


```python
test=Data.loc[(Data.tempsdg13_02 == "SDG13_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2



```python
# Term lists
termlist13_2c = ["global temperatur", "surface temperature", "sea-level", "sea level", "sea ice", "glacial", "glaciers", "permafrost", "ocean acidification", "ocean heat content",
                 "global oppvarming", "overflatetemperatur", "havnivå", "havis", "glasial", "isbre", "havforsuring"]

termlist13_2d = ["action", "sustainab", "adapt", "cope", "coping", "resilience", "mitigat", "impact", "effect",  "consequence", "influence", "vulnerab",
                 
                 "handling", "bærekraft", "berekraft", "takl", "klare", "greie", "fikse", "overkomme", "tilpas", "mink", "demp", "reduser", "reduksjon", "innflytelse", "innvirkning",
                 "innverknad", "påvirk", "påverk", "betydning", "effekt", "konsekvens", "sårbar"]

termlist13_2e = ["national", "state", "federal", "domestic", "sectoral", "multi level", "multilevel",
                 "nasjonal", "stat", "føderal", "delstat", "fylke", "innenlands", "innalands", "innanlands", "sektor", "kommune"]

termlist13_2f = ["program", "strategy", "framework", "initiativ", "plan", "policy", "policies", "law", "legislat", "governance", "mandat",
                 "nationally determined contribution", "adaptation communication", "monitoring and evaluation", "adaptation committee",
                 
                 "strategi", "rammeverk", "politikk", "retningslin", "lov", "lovgiv", "styring", "ledelse", "leiing",
                 "nasjonalt fastsatt bidrag", "nasjonalt fastsatte bidrag", "nasjonalt fastsette bidrag", "tilpasningskommunikasjon", "tilpassingskommunikasjon", "komite"]

phrasedefault13_2c = r'(?:{})'.format('|'.join(termlist13_2c))
phrasedefault13_2d = r'(?:{})'.format('|'.join(termlist13_2d))
phrasedefault13_2e = r'(?:{})'.format('|'.join(termlist13_2e))
phrasedefault13_2f = r'(?:{})'.format('|'.join(termlist13_2f))
```


```python
#Search13_2cdef
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault13_2c, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault13_2d, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault13_2e, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault13_2f, na=False, case=False))
),"tempsdg13_02"] = "SDG13_02"

print("Number of results = ", len(Data[(Data.tempsdg13_02 == "SDG13_02")]))  
```


```python
test=Data.loc[(Data.tempsdg13_02 == "SDG13_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
# Term lists
termlist13_2g = ["Kyoto protocol", "kyoto", "Paris agreement", "cop 21", "cop21", "cop 22", "cop22", "cop 23", "cop23",
                 "cop 24", "cop24", "cop 25", "cop25", "cop 26", "cop26", "cop 27", "cop27", "cop28",
                 "unfccc", "United Nations Framework Convention on Climate Change", "Cancun", "adaptation framework",
                 
                 "kyotoprotokoll", "parisavtale", "paris-avtale", "parisavtala", "paris-avtala", "klimakonvensjon"]

termlist13_2gtrunk = ["Paris"]

termlist13_2h = ["national", "state", "federal", "domestic", "sectoral", "multi level", "multilevel"
                 "nasjonal", "stat", "føderal", "delstat", "fylke", "innenlands", "innalands", "innanlands", "sektor", "kommune"]

termlist13_2i = ["program", "strategy", "framework", "initiativ", "plan", "policy", "policies", "law", "legislat", "governance", "mandat",
                 "nationally determined contribution", "adaptation communication", "monitoring and evaluation", "adaptation committee",
                 
                 "strategi", "rammeverk", "politikk", "retningslin", "lov", "lovgiv", "styring", "ledelse", "leiing",
                 "nasjonalt fastsatt bidrag", "nasjonalt fastsatte bidrag", "tilpasningskommunikasjon", "komite"]

phrasedefault13_2g = r'(?:{})'.format('|'.join(termlist13_2g))
phrasespecific13_2gtrunk = r'\b(?:{})\b'.format('|'.join(termlist13_2gtrunk))
phrasedefault13_2h = r'(?:{})'.format('|'.join(termlist13_2h))
phrasedefault13_2i = r'(?:{})'.format('|'.join(termlist13_2i))
```


```python
#Search 13_2ghi
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault13_2g, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific13_2gtrunk, na=False, case=False))
    )
    & ((Data['result_title'].str.contains(phrasedefault13_2h, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_2i, na=False, case=False)))
),"tempsdg13_02"] = "SDG13_02"

print("Number of results = ", len(Data[(Data.tempsdg13_02 == "SDG13_02")]))  
```


```python
test=Data.loc[(Data.tempsdg13_02 == "SDG13_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13.3

13.3 Improve education, awareness-raising and human and institutional capacity on climate change mitigation, adaptation, impact reduction and early warning

Styrkje evna enkeltpersonar og institusjonar har til å redusere klimagassutslepp, tilpasse seg til og redusere konsekvensane av klimaendringar og varsle tidleg, og dessutan styrkje utdanninga og bevisstgjeringa om dette.


```python
# Term lists
termlist13_3a1 = ["climate", "climatic change", "global warming", "sea level rise", "rising sea level",
                  "klima", "global oppvarming", "havnivåstigning"]

termlist13_3b1 = ["action", "mitigat", "adaptive capacity", "capacity to adapt", "resilien", "early warning", "warning system", 
                  "preparedness", "risk", "vulnerab", "awareness",
                  "climate education", "climate sensitive education", "climate change education", "climate literacy", "solution", "problem",

                 "handl", "mink", "demp", "reduser", "reduksjon", "tilpas", "takl", "klare", "greie", "fikse", "overkomme", "tidlig varsling", "tidleg varsling", "varslingssystem",
                 "forbered", "førebu", "risik", "sårbar", "bevisst", "oppmerks",
                 "klimautdann", "klimaopplær", "klimakomp", "løsning", "løysing"]

termlist13_3c1 = ["reduc", "minimi", "decreas", "limit", "alleviat",
                 "reduser", "reduksjon", "minimer", "mink", "grens", "lett"]
termlist13_3d1 = ["impact", "effect", "consequence",
                 "innflytelse", "innvirkning", "innverknad", "påvirk", "påverk", "betydning", "effekt", "konsekvens", "følge", "følgje"]

termlist13_3e1 = ["sustainab","adapt", "cope", "coping",
                 "bærekraft", "berekraft", "tilpas", "takl", "klare", "greie", "fikse", "overkomme"]

termlist13_3f1 = ["reduc", "minimi", "decreas", "limit", "alleviat", "lower", "mitigate", "tackl", "combat", "prevent", "stop", "avoid", "capture", "storage", "store", "storing", "sequestrat",
                 "reduser", "reduksjon", "minimer", "mink", "grens", "lett", "takl", "klare", "greie", "fikse", "overkomme", "kjempe", "hindr", "stopp", "stogg", "unngå", "fang", "lagr", "isoler", "isolasjon"]
termlist13_3g1 = ["GHG", "greenhouse gas", "carbon footprint", "CO2 footprint", "carbon emission", "CO2 emission",
                 "drivhusgass", "klimagass", "karbonfotavtrykk", "karbonavtrykk", "karbonutsl", "karbondioksidutsl", "co2-utsl"]
termlist13_3h1 = ["methane", "CH4", "nitrous oxide", "NOX", "N2O", "CO2", "carbon", "HFCs", "PFCs", "sulphur hexafluoride", "sulfur hexafluoride", "SF6",
                  "metan", "nitrogenoksid", "karbon", "svovel"]

termlist13_3inot = ["motivational climate", "organisational climate", "organizaional climate", "learning climate", "education climate", "emotional climate", "family climate",
                  "motivasjonsklima", "organisasjonsklima", "arbeidsklima", "læringsklima", "følelsesmessig klima", "familieklima"]

phrasedefault13_3a1 = r'(?:{})'.format('|'.join(termlist13_3a1))
phrasedefault13_3b1 = r'(?:{})'.format('|'.join(termlist13_3b1))
phrasedefault13_3c1 = r'(?:{})'.format('|'.join(termlist13_3c1))
phrasedefault13_3d1 = r'(?:{})'.format('|'.join(termlist13_3d1))
phrasedefault13_3e1 = r'(?:{})'.format('|'.join(termlist13_3e1))
phrasedefault13_3f1 = r'(?:{})'.format('|'.join(termlist13_3f1))
phrasedefault13_3g1 = r'(?:{})'.format('|'.join(termlist13_3g1))
phrasedefault13_3h1 = r'(?:{})'.format('|'.join(termlist13_3h1))
phrasedefault13_3inot = r'(?:{})'.format('|'.join(termlist13_3inot))
```


```python
## Search 13_3abcdefghi
Data.loc[(
    (
        ( 
            (Data['result_title'].str.contains(phrasedefault13_3a1, na=False, case=False))
            & 
            (
                (Data['result_title'].str.contains(phrasedefault13_3b1, na=False, case=False))
                |((Data['result_title'].str.contains(phrasedefault13_3c1, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_3d1, na=False, case=False)))
            )
        )
        |((Data['result_title'].str.contains(phrasedefault13_3a1, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_3e1, na=False, case=False)))
        |((Data['result_title'].str.contains(phrasedefault13_3f1, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_3g1, na=False, case=False)))
        |
        (
            (Data['result_title'].str.contains(phrasedefault13_3a1, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault13_3f1, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault13_3h1, na=False, case=False))
        )
    )
    & (~Data['result_title'].str.contains(phrasedefault13_3inot, na=False, case=False))
),"tempsdg13_03"] = "SDG13_03"

print("Number of results = ", len(Data[(Data.tempsdg13_03 == "SDG13_03")]))

```


```python
test=Data.loc[(Data.tempsdg13_03 == "SDG13_03"), ("result_id", "result_title")]
test.iloc[0:25, ]
```

### SDG 13.a
13.a Implement the commitment undertaken by developed-country parties to the United Nations Framework Convention on Climate Change to a goal of mobilizing jointly $100 billion annually by 2020 from all sources to address the needs of developing countries in the context of meaningful mitigation actions and transparency on implementation and fully operationalize the Green Climate Fund through its capitalization as soon as possible.

Gjennomføre forpliktingane som dei utvikla landa som er part i FNs rammekonvensjon om klimaendring, har teke på seg for å nå målet om i fellesskap å skaffe 100 milliardar dollar per år innan 2020 frå alle kjelder for å dekkje det behovet utviklingslanda har for å innføre føremålstenlege klimatiltak og gjennomføre dei på ein open måte, og fullt ut operasjonalisere Det grøne klimafondet ved at fondet så snart som mogleg blir tilført kapital.

#### Phrase 1


```python
# term lists
termlist13_1a = ["green climate fund", "least developed countries fund", "LDCF", "special climate change fund", "SCCF"
                 "grønt fond", "klimafond",
                 ]

phrasedefault13_1a = r'(?:{})'.format('|'.join(termlist13_1a))
```


```python
# Search
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault13_1a, na=False, case=False))
),"tempsdg13_a"] = "SDG13_0a"

print("Number of results = ", len(Data[(Data.tempsdg13_a == "SDG13_0a")]))
```


```python
test=Data.loc[(Data.tempsdg13_a == "SDG13_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
# Term lists
termlist13_a2 = ["transparency", "accountability", "governance", "allocation", "misallocation", "corruption", "operationali", "capitali,", "mobilis", "mobiliz", "contribut",
                "commitment", "negotiation", "donor", "donation", "donate",
                "transparen", "ansvarlig", "ansvarleg", "styring", "ledelse", "leiing", "korrupsjon", "muting", "bestikke", "tildel", "fordel", "utdel", "alloker", "operasjonaliser", "kapital", "mobiliser", "bidra",
                "forplikt", "forhandl", "giver", "givar", "gjevar", "donasjon", "doner"]

termlist13_a3 = ["financial mechanism", "finansiering"]
termlist13_a4 = ["UNFCC", "convention", "konvensjon"]

termlist13_a5 = ["climate financ", "climate aid", "climate loan",  "climate fund", "climate bond", "climate investment", "green climate fund", "Least Developed Countries Fund",
                "LDCF", "Special Climate Change Fund", "SCCF","adaptation fund", "adaptation financ",
                 
                "klimafinans", "klimahjelp", "klimastø", "klimalån", "klimafond", "klimaobligasjon", "klimainvesteringsfond", "grønt fond", "klimafond", "tilpasningsfond", "tilpassingsfond",
                "tilpasningsfinans", "tilpassingsfinans"]

termlist13_a6 = ["mitigat", "green", "climate",
                "mink", "demp", "reduser", "reduksjon", "grøn", "klima"]

termlist13_a7 = ["financ", "fund", "invest",
                "finans", "fond"]
termlist13_a8 = ["economic", "financial", "monetary",
                  "økonomisk", "finans", "penge"]
termlist13_a9 = ["support", "assist", "resource",
                  "støtte", "stønad", "ressurs"]
termlist13_a10 = ["ODA", "cooperation fund", "development spending",
                  "samarbeidsfond", "bistandsutgift", "bistandsmid"]
termlist13_a11 = ["international", "development", "foreign",
                  "internasjonal", "utvikling", "bistand", "utenland", "utland", "utaland"]
termlist13_a12 = ["aid", "assistance", "finance", "grant", "investment",
                  "hjelp", "støtte", "stønad", "assistanse", "bistand", "finans", "bevilgning", "bevilling", "tilskudd", "tilskot", "invester"]

termlist13_a13 = ["climate change", "global warming", "climate action", "climate mitigation", "climate adaptation", "climate financ", "climate aid", "climate loan", "climate fund", "climate bond",
                  "green climate fund", "Least Developed Countries Fund",
                  "LDCF", "Special Climate Change Fund", "SCCF","adaptation fund", "adaptation financ", "low carbon"
                  
                  "klimaendr", "global oppvarming", "klimahandling", "klimatilpas", "klimafinans", "klimahjelp", "klimastø", "klimalån", "klimafond", "klimaobligasjon", "grønt fond", "klimafond", "tilpasningsfond", "tilpassingsfond",
                  "tilpasningsfinans", "tilpassingsfinans", "lavkarbon", "lågkarbon"]

phrasedefault13_a2 = r'(?:{})'.format('|'.join(termlist13_a2))
phrasedefault13_a3 = r'(?:{})'.format('|'.join(termlist13_a3))
phrasedefault13_a4 = r'(?:{})'.format('|'.join(termlist13_a4))
phrasedefault13_a5 = r'(?:{})'.format('|'.join(termlist13_a5))
phrasedefault13_a6 = r'(?:{})'.format('|'.join(termlist13_a6))
phrasedefault13_a7 = r'(?:{})'.format('|'.join(termlist13_a7))
phrasedefault13_a8 = r'(?:{})'.format('|'.join(termlist13_a8))
phrasedefault13_a9 = r'(?:{})'.format('|'.join(termlist13_a9))
phrasedefault13_a10 = r'(?:{})'.format('|'.join(termlist13_a10))
phrasedefault13_a11 = r'(?:{})'.format('|'.join(termlist13_a11))
phrasedefault13_a12 = r'(?:{})'.format('|'.join(termlist13_a12))
phrasedefault13_a13 = r'(?:{})'.format('|'.join(termlist13_a13))                                                                                   
```


```python
# Search
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault13_a2, na=False, case=False))
            |((Data['result_title'].str.contains(phrasedefault13_a3, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_a4, na=False, case=False)))
        )
        &
        (
            (Data['result_title'].str.contains(phrasedefault13_a5, na=False, case=False))
            |
            (
                (Data['result_title'].str.contains(phrasedefault13_a6 , na=False, case=False))
                &
                (
                    (Data['result_title'].str.contains(phrasedefault13_a7 , na=False, case=False))
                    |((Data['result_title'].str.contains(phrasedefault13_a8 , na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_a9 , na=False, case=False)))
                    |(Data['result_title'].str.contains(phrasedefault13_a10 , na=False, case=False))
                    |((Data['result_title'].str.contains(phrasedefault13_a11 , na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_a12, na=False, case=False)))
                )
            )
        )
    )
    & ((Data['result_title'].str.contains(phrasedefault13_a13, na=False, case=False)))
),"tempsdg13_a"] = "SDG13_0a"

print("Number of results = ", len(Data[(Data.tempsdg13_a == "SDG13_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg13_a == "SDG13_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
termlist13_a14 = ["annex II party", "annex II parties", "developed contr", "developed nation", "oecd"]

phrasedefault13_a14 = r'(?:{})'.format('|'.join(termlist13_a14))
```


```python
# Search
Data.loc[(
    (
        (
            (Data['LMICs']==True)
            |(Data['result_title'].str.contains(phrasedefault13_a14 , na=False, case=False))
        )
        &
        (
            (Data['result_title'].str.contains(phrasedefault13_a5, na=False, case=False))
            |
            (
                (Data['result_title'].str.contains(phrasedefault13_a6 , na=False, case=False))
                &
                (
                    (Data['result_title'].str.contains(phrasedefault13_a7 , na=False, case=False))
                    |((Data['result_title'].str.contains(phrasedefault13_a8 , na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_a9 , na=False, case=False)))
                    |(Data['result_title'].str.contains(phrasedefault13_a10 , na=False, case=False))
                    |((Data['result_title'].str.contains(phrasedefault13_a11 , na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_a12, na=False, case=False)))
                )
            )
        )
    )
    & ((Data['result_title'].str.contains(phrasedefault13_a13, na=False, case=False)))
),"tempsdg13_a"] = "SDG13_0a"

print("Number of results = ", len(Data[(Data.tempsdg13_a == "SDG13_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg13_a == "SDG13_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13.b
13.b Promote mechanisms for raising capacity for effective climate change-related planning and management in least developed countries and small island developing States, including focusing on women, youth and local and marginalized communities.

Fremje mekanismar for å styrkje evna til effektiv klimarelatert planlegging og forvaltning i dei minst utvikla landa og små utviklingsøystatar, mellom anna med vekt på kvinner, ungdom og lokale og marginaliserte samfunn.


```python
termlist13_b1 = ["climate",
                 "klima"]
termlist13_b2 = ["strateg", "policy", "policies", "plan", "management", "adaptation communication",
                 "politikk", "retningslin", "ledelse", "leiing", "styring", "tilpasningskommunikasjon", "tilpassingskommunikasjon"]

termlist13_b3 = ["nationally determined contribution", "green climate fund", "least developed countries fund", "LDCF", "special climate change fund", "sccf", "adaptation fund", "adaptation financ",
                 "nasjonalt fastsatt bidrag", "nasjonalt fastsatte bidrag", "klimafond"]

termlist13_b4 = ["capacity", "capabilit", "educat", "curriculum", "curricula", "teacher training", "climate literacy", "research", "knowledge", "skills",
                 "tools", "competenc", "expertise", "training", "awareness", "responsibilit", "infrastructure", "technolog", "early warning system",
                 "communication", "collaboration", "cooperation", "co operation", "social network", "information network",
                 "economic resources", "financial resources", "human resource",

                 "kapasitet", "evne", "utdann", "opplær", "pensum", "læreplan", "fagplan", "emneplan", "studieplan", "lærerutdann", "lærarutdann", "klimakompetanse", "forskning", "forsking", "kunnskap", "ferdighet", "ferdigheit",
                 "verktøy", "kompetanse", "ekspertise", "bevisst", "medvett", "medvit", "ansvar", "infrastruktur", "teknolog", "tidlig varsling", "tidleg varsling", "varslingssystem",
                 "kommunikasjon", "samarbeid", "sosiale nettverk", "informasjonsnettverk",
                 "økonomiske ressurs", "finansielle ressurs", "menneskelige ressurser", "menneskelege ressursar"]

termlist13_b5 = ["institutional", "administrativ", "policy", "governance",
                 "institusjonell", "politikk", "retningslin", "ledelse", "leiing", "styring"]
termlist13_b6 = ["structure", "values", "practices", "arrangement", "resources",
                 "struktur", "verdi", "praksis", "ressurs"]

termlist13_b7 = ["climate", "global warming", "climatic change", "sea level rise",
                 "klima", "global oppvarming", "havnivåstigning" ]

termlist13_b8 = ["action", "sustainab", "mitigat", "adapt", "cope", "coping", "resilience", "early warning", "warning system", "preparedness", "risks", "vulnerab", "awareness",
                 "climate education", "climate sensitive education", "climate change education", "climate literacy", "solutions", "problem", "manag",
                 
                 "handl", "bærekraft", "berekraft", "mink", "demp", "reduser", "reduksjon", "tilpas", "takl", "klare", "greie", "fikse", "overkomme","tidlig varsling", "tidleg varsling",
                 "varslingssystem", "forbered", "førebu", "risik", "sårbar", "bevisst", "medvit", "medvett", "klimautdann", "klimakompet", "løsning", "løysing", "styring", "lede", "leie", "leiing"
                ]

phrasedefault13_b1 = r'(?:{})'.format('|'.join(termlist13_b1))
phrasedefault13_b2 = r'(?:{})'.format('|'.join(termlist13_b2))
phrasedefault13_b3 = r'(?:{})'.format('|'.join(termlist13_b3))
phrasedefault13_b4 = r'(?:{})'.format('|'.join(termlist13_b4))
phrasedefault13_b5 = r'(?:{})'.format('|'.join(termlist13_b5))
phrasedefault13_b6 = r'(?:{})'.format('|'.join(termlist13_b6))
phrasedefault13_b7 = r'(?:{})'.format('|'.join(termlist13_b7))
phrasedefault13_b8 = r'(?:{})'.format('|'.join(termlist13_b8))
```


```python
# Search in LDCs and SIDS
Data.loc[(
    (
        (
            ((Data['result_title'].str.contains(phrasedefault13_b1, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_b2, na=False, case=False)))
            |(Data['result_title'].str.contains(phrasedefault13_b3, na=False, case=False))
        )
        |
        (
            (
                (Data['result_title'].str.contains(phrasedefault13_b4, na=False, case=False))
                |((Data['result_title'].str.contains(phrasedefault13_b5, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_b6, na=False, case=False)))
            )
            & ((Data['result_title'].str.contains(phrasedefault13_b7, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_b8, na=False, case=False)))
        )
    )
    & (Data['LDCSIDS']==True)
),"tempsdg13_b"] = "SDG13_b"

print("Number of results = ", len(Data[(Data.tempsdg13_b == "SDG13_b")]))
```


```python
test=Data.loc[(Data.tempsdg13_b == "SDG13_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13 mentions



```python
# Term lists
termlist13_1 = ["SDG 13", "SDGs 13", "SDG13", "sustainable development goal 13",
                "bærekraftsmål 13", "berekraftsmål 13"]
termlist13_2 = ["sustainable development goal", 
                "bærekraftsmål", "berekraftsmål"]
termlist13_3 = ["goal 13", 
                "mål 13"]
termlist13_4 = ["sustainable development goal", "SDG", "goal 13", 
                "bærekraftsmål", "berekraftsmål", "mål 13"]
termlist13_5 = ["climate", 
                "klima"]
termlist13_6 = ["climate action", 
                "stoppe klimaendringene", "stoppe klimaendringane"]

phrasedefault13_1 = r'(?:{})'.format('|'.join(termlist13_1))
phrasedefault13_2 = r'(?:{})'.format('|'.join(termlist13_2))
phrasedefault13_3 = r'(?:{})'.format('|'.join(termlist13_3))
phrasedefault13_4 = r'(?:{})'.format('|'.join(termlist13_4))
phrasedefault13_5 = r'(?:{})'.format('|'.join(termlist13_5)) 
phrasedefault13_6 = r'(?:{})'.format('|'.join(termlist13_6))     
```


```python
## Search 13_123456
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault13_1, na=False, case=False))
    |((Data['result_title'].str.contains(phrasedefault13_2, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_3, na=False, case=False))) 
    |((Data['result_title'].str.contains(phrasedefault13_4, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault13_5, na=False, case=False)))
    |(Data['result_title'].str.contains(phrasedefault13_6, na=False, case=False))
),"tempmentionsdg13"] = "SDG13"

print("Number of results = ", len(Data[(Data.tempmentionsdg13 == "SDG13")]))
```


```python
test=Data.loc[(Data.tempmentionsdg13 == "SDG13"), ("result_id", "result_title")]
test.iloc[5:10, ]
```

## SDG 14

Webpages about SDG targets from the UN Association of Norway were used to get target translations and to help with Norwegian terms (https://www.fn.no/om-fn/fns-baerekraftsmaal/livet-i-havet).

We have also used "Realfagstermer", a controlled vocabulary for English and Norwegian scientific terms from the University of Oslo and University of Bergen - https://app.uio.no/ub/emnesok/realfagstermer/search

A website with Norwegian and English names for international environmental agreements from the Norwegian Environment Agency was used to help translate international agreement/convention names (https://www.miljodirektoratet.no/regelverk/konvensjoner/; accessed 24/01/23)

### Marine terms

Used together with most (but not all) targets to try and limit the results to the marine environment. Done by creating a T/F column ("marine_terms") that can be combined with other searches. T = contains a word indicating it is about the marine environment. 


```python
#Term lists

termlist14_marine1 = ["marine", "mariculture", "barents sea", "norwegian sea",
                     "seabed", "seafloor", "seamount", "hydrothermal vent", "cold seep", "continental shelf", "continental shelves", "continental slope", 
                     "subtidal", "intertidal", "deep sea", "bathyal", "abyssal",
                     "rocky shore", "beach", "salt marsh", "mud flat", "mudflat", "tidal flat",
                     "estuar", "fjord", 
                     "sea ice",
                     "sea life", "sealife", "mangrove", "kelp bed", "kelp forest", "seagrass", "seaweed", "macroalga", 
                     "sponge ground", "organic fall", "reef", 
                     "coastal communit", "coastal zone management",
                     "offshore",
                      
                      "sjøområd", "havområd", "havbruk", "havforsuring", "Skagerrak", 
                      "sjøbunn", "sjøbotn", "havbunn", "havbotn", "sjøfjell", "hydrotermisk skorstein", "hydrotermiske skorstein", "hydrotermisk ventil", "midhavsrygg", "kontinentalskråning", "kontinentalhylle",
                      "submarin", "fjære", "fjøre", "tidevann", "tidevatn", "havdyp", "havdjup", "dyphav", "djuphav", 
                      "sandstrand", "strandeng", "saltmarsk", "saltvannssump",
                      "havis", "sjødyr", "sjøgress", "sjøgras", "korall", 
                      "kystsamfunn", "kystson",
                      "utaskjærs",
                      "skipsfart"]
                     #Difficult because "Fjære"(NO) is also a local municipality
                     #"tidevann"(NO) will cover several other terms, like tidevannssonen
                     #"skipsfart"(NO) was added here as in Norwegian it is likely to be used in a marine context. In English, "ship" is combined with other terms.
                     #In Norwegian I have added "havbruk"(NO) as this is aquaculture specifically in the sea, and "havforsuring"(NO) (as "hav" is difficult to use alone). 
                     #Also relevant geographic areas (e.g. Skagerrak), but some will be found by "havet"(NO) below (e.g. Barentshavet).

termlist14_marine2 = ["ocean", "oceans", "oceanogra.*", "seas", 
                      "marin", "oseanografi.*", "hav", "havet", "verdenshav", "sjø", "sjøen", "tang", "tare"]
                      #"marin"(EN&NO), "tang" (NO), "tare"(NO) are added here instead of untruncated in termlist_marine1 because it is part of other words (e.g. marinate)

termlist14_marine3 = ["sea", "coast", "coastal", "tidal",
                      "sjø.*", "kyst.*", "tideva.*"]
                      #"tideva"(NO) covers both tidevatn and tidevann while excluding "tide"

termlist14_marine4 = ["habitat", "ecosystem", "dune", "wetland", "marsh", "bay", "lagoon", "gulf", "water", "current", "pelagi",
                     "fish", "shrimp", "shellfish", "aquacultur",
                      "harbour", "harbor", "port", "maritim", "ship",

                      "leveområd", "økosystem", "våtmark", "sumpmark", "viker", "bukter", "strøm",
                      "fisk", "akvakultur", 
                      "havn", "båt", "elvemunn"] 
                     #In the original string, "sea" and "coast" etc. were combined with this set to remove noise (i.e. coastal cities)
                     #However, in a title search, I think we lose more relevant than we get noise, so I do not combine with this set.
                        #"elvemunn"(NO) is moved here as used with rivers into lakes also
                        #"maritim", "pelagi" cover both the Norwegian and English terms
                        #"bay" and "ship" are potentially problematic with free truncation, but combined with the terms in marine3 don't seem to cause issues

termlist14_marine5 = ["marine", "ocean", "oceans", "oceanogra.*", "estuar.*", "deep sea", "sea", 
                      "havforsk.*", "havbruk.*"] 
                      #Journal titles
                      #Using "hav"(NO) alone is difficult, even with no truncation, because in Norwegian it is so often in combined words

phrasedefault14_marine1 = r'(?:{})'.format('|'.join(termlist14_marine1))
phrasespecific14_marine2 = r'\b(?:{})\b'.format('|'.join(termlist14_marine2))
phrasespecific14_marine3 = r'\b(?:{})\b'.format('|'.join(termlist14_marine3))
phrasedefault14_marine4 = r'(?:{})'.format('|'.join(termlist14_marine4))
phrasespecific14_marine5 = r'\b(?:{})\b'.format('|'.join(termlist14_marine5))
```


```python
Data["marine_terms"] = (
    (Data['result_title'].str.contains(phrasedefault14_marine1, na=False, case=False))
    |(Data['result_title'].str.contains(phrasespecific14_marine2, na=False, case=False))
    | (Data['result_title'].str.contains(phrasespecific14_marine3, na=False, case=False)) #& (Data['result_title'].str.contains(phrasedefault14_marine4, na=False, case=False)))
    | (Data['journal'].str.contains(phrasespecific14_marine5, na=False, case=False))
    )
#In the original string, "sea" and "coast" etc. were combined with this set to remove noise (i.e. coastal cities)
#However, in a title search, we seem to lose more relevant than we get noise, so we do not combine with this set (commented out above).

len(Data.loc[Data['marine_terms']])
```


```python
#Results
test=Data.loc[Data['marine_terms']]
test.iloc[0:10, [0,4,5,6,8]]
```

### SDG 14.1

*14.1 By 2025, prevent and significantly reduce marine pollution of all kinds, in particular from land-based activities, including marine debris and nutrient pollution*

*Innen 2025 forhindre og i betydelig grad redusere alle former for havforurensning, særlig fra landbasert virksomhet, inkludert marin forsøpling og utslipp av næringssalter*

#### Phrase 1/2/3


```python
#Termlists
termlist14_1a = ["pollut", 
                 "sewage","sewer", "eutrophicat","excess nutrient","excessive nutrient","effluent","runoff","waste","discharge",
                 "littering","garbage patch","debris",
                 "microplastic","micro plastic","nanoplastic","nano plastic","plastic waste","plastic particles",
                 "heavy metal","toxic metal","mercury","arsenic","cadmium","chromium","copper","nickel",
                 "organotin","tributyltin","TBT","mining","mine tailing",
                 "contaminant","bioaccumula","bioconcentrat","ecotox","toxic chemical",
                 "endocrine disrupting chemical", "persistent organic pollutant","pesticid","herbicide",
                 "polychlorinated biphenyl","hexachlorocyclohexane","hexachlorobenzene","hexachlorobutadiene",
                 "pentachlorobenzene","pentachlorophenol","pentachloroanisole","hexabromocyclododecane",
                 "polybrominated diphenyl ether","perflurochemicals","PFAS","endosulfan", "polycyclic aromatic hydrocarbon",
                 "oil spill", "crude oil",

                 "forurens", "forurein",
                 "utslipp", "kloakk", "eutrofier", "overgjødsling", "overflatevann", "overflatevatn", "avrenning", "næringssalt",
                 "søppel", "avfall", #"farlig avfall", "kjemikalieavfall", "radioaktivt avfall", 
                 "mikroplast", "plastpartik", #"plastavfall",
                 "tungmetall", "kvikksølv", "kadmium", "kobber", "nikkel", "arsenikk",
                 "tinnorganiske", "organiske tinnforbindelse", #"gruveavfall",
                 "bioakkumuler", "miljøtoksikologi",
                 "miljøgift", "hormonforstyr", "insektmiddel", "insektmidler", "plantevernmid",
                 "oljesøl", "oljeutslipp"]
                 #Can add "wastewater","waste water" back again if "waste" is too general alone
                 #"pesticid" will find Norwegian-ifications of this word.
                 #"avfall" (NO), after testing, is ok to use alone, thus the specific terms are commented out above.

termlist14_1b_case = ["PCB","DDT","PAH"] 

termlist14_1c = ["litter", 
                 "bly", "arsen", "krom", "tinn", "plast"]
                 #"Litter" needs specific truncation because it is part of "litteratur" in Norwegian
                 #These Norwegian heavy metals are short words and need to prevent truncation

termlist14_1d = ["oil", "lead",
                 "olje", "kjemikal.*"]

termlist14_1e = ["contamina", "toksis"]

termlist14_1not = ["PM2.5","PM10","leaf litter"] 

phrasedefault14_1a = r'(?:{})'.format('|'.join(termlist14_1a))
phrasedefault14_1b_case = r'(?:{})'.format('|'.join(termlist14_1b_case))
phrasespecific14_1c = r'\b(?:{})\b'.format('|'.join(termlist14_1c))
phrasespecific14_1d = r'\b(?:{})\b'.format('|'.join(termlist14_1d))
phrasedefault14_1e = r'(?:{})'.format('|'.join(termlist14_1e))
phrasedefault14_1not = r'(?:{})'.format('|'.join(termlist14_1not))
```


```python
#Search 
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault14_1a, na=False, case=False))
            | (Data['result_title'].str.contains(phrasedefault14_1b_case, na=False, case=True)) #case = True
            | (Data['result_title'].str.contains(phrasespecific14_1c, na=False, case=False))
            | ((Data['result_title'].str.contains(phrasespecific14_1d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_1e, na=False, case=False)))
        )
        & (~Data['result_title'].str.contains(phrasedefault14_1not, na=False, case=False))
    ) & (Data['marine_terms']==True)
),"tempsdg14_01"] = "SDG14_01"

print("Number of results = ", len(Data[(Data.tempsdg14_01 == "SDG14_01")]))
```


```python
test=Data.loc[(Data.tempsdg14_01 == "SDG14_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.2

*14.2 By 2020, sustainably manage and protect marine and coastal ecosystems to avoid significant adverse impacts, including by strengthening their resilience, and take action for their restoration in order to achieve healthy and productive oceans*

*Innen 2020 forvalte og beskytte økosystemene i havet og langs kysten på en bærekraftig måte for å unngå betydelig skadevirkninger, blant annet ved å styrke økosystemenes motstandsevne og ved å iverksette tiltak for å gjenoppbygge dem, slik at havene kan bli sunne og produktive*

#### Phrase 1/2


```python
#Termlists
termlist14_2a = ["marine reserve", "ocean reserve", "marine sanctuar", "marine park", "particularly sensitive sea area","marine conservation",
                 "marine spatial planning",
                 "coastal zone management","integrated coastal zone planning","coastal resources management",
                 "locally managed marine area",

                 "marint vernområde","marine vernområde","marine verneområde","marine reservat","marint vern",
                 "integrert kystsone", "kystplanlegging", "kystsoneforvaltning"]
termlist_14_2acase = ["LMMA.*", "NTMR","ICZM", "LSMPA.*", "MPA", "MPAs"] #can search case sensitive
            
#Above are terms that are specific to the marine environment
#In the rest of the term lists, the terms need combining with marine terms

termlist14_2b = ["nature reserve", 
                 "spatial management", "community based management","resilience based management",
                 "herbivore management area", 
                 "ecosystem-based", "area-based manag", "area-based approach",
                 "sustainable management", "sustainable governance",
                 "no-take area", "no-take zone", "no-take reserve",

                 "naturreservat", "biotopvernområde", "nasjonalpark", "bevarte område", "bevart område", "bevaringsområde",
                 "økosystembasert forvaltning", "økosystemtilnærming", "økosystembasert styring", "forvaltningsplaner",
                 "samfunnsforvalt", "bærekraftig forvalt", "berekraftig forvalt", "arealforvalt", "bærekraftig ledelse", "berekraftig leiing",
                 "fiskeforbud", "fiskevernsone"]

termlist14_2c = ["protect","conserve","conservation","conserves","conserving",
                "vernet", "verne", "verna", "vern av", "bevare", "bevaring", "frede", "freda", "fredning", "beskytt" ]

termlist14_2d = ["area", "zone", "habitat","ecosystem",
                "område", "sone", "miljø", "leveområd", "økosystem"]

termlist14_2not = ["Marine Predator Algorithm"] 
#This term can cause an issue if you run a search for "MPA" in titles - but not using "MPA" loses relevant results. 
# In abstracts/longer texts it sometimes works better to drop "MPA" as they normally use the full term somewhere ("protected areas")

phrasedefault14_2a = r'(?:{})'.format('|'.join(termlist14_2a))
phrasespecific14_2acase = r'\b(?:{})\b'.format('|'.join(termlist_14_2acase))
phrasedefault14_2b = r'(?:{})'.format('|'.join(termlist14_2b))
phrasedefault14_2c = r'(?:{})'.format('|'.join(termlist14_2c))
phrasedefault14_2d = r'(?:{})'.format('|'.join(termlist14_2d))
phrasedefault14_2not = r'(?:{})'.format('|'.join(termlist14_2not))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_2a, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasespecific14_2acase, na=False, case=True)) #case = True
        | (Data['result_title'].str.contains(phrasedefault14_2b, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault14_2c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_2d, na=False, case=False)))
    )
    &(Data['marine_terms']==True)
    &~(Data['result_title'].str.contains(phrasedefault14_2not, na=False, case=True))
),"tempsdg14_02"] = "SDG14_02"

print("Number of results = ", len(Data.loc[(Data.tempsdg14_02 == "SDG14_02")]))  
```


```python
test=Data.loc[(Data.tempsdg14_02 == "SDG14_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist14_2e = ["manag", "conserv", "protect", "restor", "rehabilita", "resilien",      
                 "forvalt", "verne", "verna", "vern av", "miljøvern","bevare", "bevaring", "frede", "freda", "fredning", "beskytt", "gjenoppbygg", "restaurer", "bærekraftig bruk", "berekraftig bruk"]
                 #"vernet"(NO) will also find "vernetiltak"

termlist14_2f = ["habitat","ecosystem","ecological communit",
                 "mangrove", "kelp", "seagrass", "seaweed", "macroalga", "sponge ground", "reef", "coral", 
                 "salt marsh", "mud flat", "mudflat", "tidal flat",
                 "estuar", "fjord", "coastal dune", "coastal wetland", "coastal water", 
                 "environmental function", "environmental quality", "environmental stabil", "environmental resilience",
                 "ocean health", "ocean function", "ocean resilience",
                 "water quality",
                 "diversity", "tipping point", "extinction", "key species", "foundation species", "keystone species", "habitat-forming",
                 "productivity", "food production", "fish stock", "fishery", "fisheries", "aquaculture",
                 "habitats directive","Conservation of Antarctic Marine Living Resources", 
                 "Lima convention","Nairobi convention","Noumea convention","Barcelona convention","World heritage convention","European landscape convention",
                 "International coral reef initiative",

                "leveområd", "miljø", "økosystem", "samfunn",
                "sjøgress", "makroalge", "korall", "saltmarsker", "sandstrand", "strandeng",
                "havbunn", "sjøbunn", "sjøfjell", "hydrotermisk skorstein", "hydrotermiske skorstein", "hydrotermisk ventil", "midhavsrygg", "kontinentalskråning", "kontinentalhylle",
                "vannkvalitet", "resiliens",
                "mangfold", "mangfald", "diversitet", "vippepunkt", "nøkkelart", "flaggskipsart", "paraplyart", 
                "produktivitet", "mat produksjon", "fiskebestand", "fiskeri", "havbruk", "akvakultur",
                "habitatdirektiv", "Lima-konvensjonen","Nairobi-konvensjonen","Noumea-konvensjonen","Barcelona-konvensjonen","verdensarvkonvensjonen","Landskapskonvensjonen",
                "naturmangfoldloven", "områdevern", "artsforvaltning"]
                #added Norwegian-specific legislation

termlist14_2ftrunc = ["tare.*", "tang", "tangart.*"] #Norwegian terms from 2f that need prevent truncation

termlist14_2hcase = ["BBNJ", "CBD", "HELCOM", "OSPAR", "UNEP", "CCAMLR"]

phrasedefault14_2e = r'(?:{})'.format('|'.join(termlist14_2e))
phrasedefault14_2f = r'(?:{})'.format('|'.join(termlist14_2f))
phrasespecific14_2ftrunc = r'\b(?:{})\b'.format('|'.join(termlist14_2ftrunc))
phrasedefault14_2hcase = r'(?:{})'.format('|'.join(termlist14_2hcase))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_2hcase, na=False, case=True)) #case=T
        | ((Data['result_title'].str.contains(phrasedefault14_2e, na=False, case= False)) & (Data['result_title'].str.contains(phrasedefault14_2f, na=False, case=False)))
        | ((Data['result_title'].str.contains(phrasedefault14_2e, na=False, case= False)) & (Data['result_title'].str.contains(phrasespecific14_2ftrunc, na=False, case=False)))
    )
    &(Data['marine_terms']==True)
),"tempsdg14_02"] = "SDG14_02"

print("Number of results = ", len(Data.loc[(Data.tempsdg14_02 == "SDG14_02")])) 
```


```python
test=Data.loc[(Data.tempsdg14_02 == "SDG14_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.3
*14.3 Minimize and address the impacts of ocean acidification, including through enhanced scientific cooperation at all levels*

*Begrense mest mulig og sørge for håndtering av konsekvensene av havforsuring, blant annet gjennom styrket vitenskapelig samarbeid på alle nivåer*

Compared to the original string, we have added the term "monitoring" ("overvåk"). This is somewhat of an expansion; the original string was very limited to terms to do with impacts. If one can consider monitoring as a way of "addressing" impacts then it should be added to the original string too. 


```python
#Termlists
termlist14_3a = ["impact", "effect", "affect", "respons", "consequence",
                 "results in", "changes", "alters", "altering", "changing",
                 "sensitiv", "vulnerab", "threat",
                 "resilien", "coping", "toleran",
                 "calcif", "carbonate", "aragonit", "calcite", 
                 "extinct", "adapt", "competiti", "recruit", "surviv", "reproduc",
                 "monitor",

                 "påvirk", "impakt", "konsekvens", "effekt",
                 "resultat", "endring", 
                 "sårbar", "truet", "truer", " trua", " trued", "stress", "tåle", 
                 "forkalk", "karbonsyre", "karbonat", "kalsit", "skjell", #"aragonit", 
                 "utrydd", "tilpass", "konkurr", "rekrutter", "overleve", "formering", "reproduksjon",
                 "overvåk", "overvak"]
                #spaces added with "trua"(NO) and "trued"(NO) on purpose to avoid truncation

termlist14_3b = ["acidi", "ocean ph", "seawater ph", "low ph", "declining ph", "decreasing ph", "decreased ph", "effect of ph", "effects of ph",
                 "forsur", "nedgangen i pH", "nedgang i ph", "lav ph", "lavere ph", "lågere ph", "surere hav", "surare hav", "surt hav"]

termlist14_3ccase = ["OA"]

phrasedefault14_3a = r'(?:{})'.format('|'.join(termlist14_3a))
phrasedefault14_3b = r'(?:{})'.format('|'.join(termlist14_3b))
phrasespecific14_3ccase = r'\b(?:{})\b'.format('|'.join(termlist14_3ccase))
```


```python
#Search 1
#Note that "havforsuring" (NO; ocean acidification) is included in the marine terms, so it should not be a problem to find works using this term even when combined with marine terms.
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_3a, na=False, case=False)) 
        & (
            (Data['result_title'].str.contains(phrasedefault14_3b, na=False, case=False)) 
            | (Data['result_title'].str.contains(phrasespecific14_3ccase, na=False, case=True)) #case = T
            )
    )
    &(Data['marine_terms']==True)
),"tempsdg14_03"] = "SDG14_03"

print("Number of results = ", len(Data.loc[(Data.tempsdg14_03 == "SDG14_03")]))  
```


```python
test=Data.loc[(Data.tempsdg14_03 == "SDG14_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.4

*14.4 By 2020, effectively regulate harvesting and end overfishing, illegal, unreported and unregulated fishing and destructive fishing practices and implement science-based management plans, in order to restore fish stocks in the shortest time feasible, at least to levels that can produce maximum sustainable yield as determined by their biological characteristics*

*Innen 2020 innføre effektive tiltak for å regulere uttaket av fiskebestandene, få slutt på overfiske og ulovlig, urapportert og uregulert fiske og ødeleggende fiskemetoder, og iverksette vitenskapelig baserte forvaltningsplaner for å gjenoppbygge fiskebestandene på kortest mulig tid, i det minste til de nivåene som kan gi høyest mulig bærekraftig avkastning ut fra bestandenes biologiske særtrekk*

#### Phrase 1/2


```python
#Termlists
termlist14_4a = ["overfish", "bycatch", "by-catch", "IUU fish", 
                 "ghost fishing", "ghost net", "ALDFG", "poison fishing",

                 "overfisk", "ulovlig fisk", "ulovlige fisk", "ulovleg fisk", "ulovlege fisk", "tjuvfiske", "bifangst", "UUU fiske", "UUU-fiske",
                 "spøkelsesfiske", "tapte garn"]

termlist14_4b = ["gear", "net", "nets",
                 "fiskeredskap.*", "fiskegarn", "havteine.*", "torskebur", "teina"]
termlist14_4c = ["abandoned", "lost", "discarded",
                 "tapt", "mistet", ]

termlist14_4d = ["trawl", "trawling",
                 "trål", "bunntrål.*", "trålfiske"]
                 #"Trål" (NO) causes problems alone with free truncation (e.g. stråle)
termlist14_4e = ["degrad", "damag", "harm",
                 "skade", "ødelag", "ødeleg"]

termlist14_4f = ["overharvest", "overexploit", "overcapacit", "collaps", "closure",
                 "illegal", "unreport", "unregulat", "corrupt", "destruct", "blast", "dynamite", "cyanid",
                 
                 "overbeskat", "kollaps", "stenge", "stenging",
                 "ulovlig", "ulovleg", "urapport", "uregulert", "korrupsj", "ødelegg", "ødelagt", "forring", "dynamitt", "eksplosiv", "tapt redskap", "tapte redskap"]
                #"cyanid" covers norwegian and english
    
termlist14_4g = ["fishing", "fisher", "shellfish", "trawl",                
                 "fiske", "skalldyr"]

phrasedefault14_4a = r'(?:{})'.format('|'.join(termlist14_4a))
phrasespecific14_4b = r'\b(?:{})\b'.format('|'.join(termlist14_4b))
phrasedefault14_4c = r'(?:{})'.format('|'.join(termlist14_4c))
phrasespecific14_4d = r'\b(?:{})\b'.format('|'.join(termlist14_4d))
phrasedefault14_4e = r'(?:{})'.format('|'.join(termlist14_4e))
phrasedefault14_4f = r'(?:{})'.format('|'.join(termlist14_4f))
phrasedefault14_4g = r'(?:{})'.format('|'.join(termlist14_4g))
```


```python
#Search 1

Data.loc[(
    (Data['result_title'].str.contains(phrasedefault14_4a, na=False, case=False)) 
    | ((Data['result_title'].str.contains(phrasespecific14_4b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_4c, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasespecific14_4d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_4e, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasedefault14_4f, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_4g, na=False, case=False)))
),"tempsdg14_04"] = "SDG14_04"

print("Number of results = ", len(Data[(Data.tempsdg14_04 == "SDG14_04")])) 
```


```python
test=Data.loc[(Data.tempsdg14_04 == "SDG14_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3

Fish species taken from The Norwegian Directorate of Fisheries https://www.fiskeridir.no/Yrkesfiske/Tall-og-analyse/Fangst-og-kvoter/Fangst/Fangst-fordelt-paa-art 


```python
#Termlists
termlist14_4h = ["manag", "planning", "governance", 
                 "restor", "stock recovery","rehabilit",
                 "sustainab", "ecosystem approach",
                 "maximum sustainable yield", 
                 "marine stewardship council", 
                 "regional fisheries management", 
                 "convention on the law of the sea", "fish stocks agreement", "code of conduct for responsible fisheries", "port state measures agreement",
                 "Management of Straddling Fish Stocks", "Management of Highly Migratory Fish Stocks", "north atlantic salmon conservation organization",
                 "deep-sea fisheries guidelines", "Management of Deep-sea Fisheries in the High Seas", 
                 "common fisheries policy", 
                 "legislation", "instrument", "strateg", "policy", "policies", "framework", "agreement", "treaty", "treaties",

                 "forvalt", "planlegg", "styring", "ledelse", "leiing",
                 "gjenoppbygg", "restaurer",
                 "bærekraftig", "berekraftig", "økosystemtilnærming","økosystembasert forvaltning",
                 "likevektsfangst",
                 "havrettskonvensjon", "Havrettstraktaten",
                 "avtalen om fiske på det åpne hav", "avtalen om havnestatstiltak",
                 "den nordatlantiske laksevernorganisasjonen",
                 "regulering av fisket etter dyphavsarter",
                 "felles fiskeripolitik",
                 "politikk", "lovverk", "regelverk", "regler", "rettningslin", "utredning", "utgreiing", "rammeverk", "avtale", "forskrift"]
termlist14_4icase = ["EBFM", "MSY", "RFMO", "UNCLOS", "CCRF", "UNFSA"]

termlist14_4jtrunc = ["law", "plan", "plans",
                      "lov", "planer"]
                
termlist14_4k = ["fish", "cod stock", "cod population", "herring", "saithe", "haddock", "mackrel", "capelin", "blue whiting", #"fishing", "fisher", "shellfish", "fish stock", "overfish",                
                 "fiske", "skalldyr", "torsk", "skrei", "kysttorsk", "sild", "sei ", "seifisk", "hyse", "makrell", "lodde ", "loddefisk", "kolmule"]
                #terms where I prevent left truncation ("orthograFISKE"). 
                #Here we have added some Norwegian fish species, taken from the Norwegian Directorate of Fisheries ("utvalgte art")
                #"sei"(NO) was however difficult to include alone, have added a space after to prevent truncation in both direction
            
termlist14_4l = ["catch",
                 "fangst"]
termlist14_4m = ["entitlement", "limit", "tolerance",
                 "begrens", "kvote"]                                
phrasedefault14_4h = r'(?:{})'.format('|'.join(termlist14_4h))
phrasedefault14_4icase = r'(?:{})'.format('|'.join(termlist14_4icase))
phrasespecific14_4j = r'\b(?:{})\b'.format('|'.join(termlist14_4jtrunc))
phrasespecific14_4k = r'\b(?:{})'.format('|'.join(termlist14_4k))
phrasedefault14_4l = r'(?:{})'.format('|'.join(termlist14_4l))
phrasedefault14_4m = r'(?:{})'.format('|'.join(termlist14_4m))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_4h, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasedefault14_4icase, na=False, case=True)) #case = True
        | (Data['result_title'].str.contains(phrasespecific14_4j, na=False, case=False))
    ) 
    &
    (
        (Data['result_title'].str.contains(phrasespecific14_4k, na=False, case=False)) 
        | ((Data['result_title'].str.contains(phrasedefault14_4l, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_4m, na=False, case=False)))
    )
),"tempsdg14_04"] = "SDG14_04"

print("Number of results = ", len(Data[(Data.tempsdg14_04 == "SDG14_04")])) 
```


```python
test=Data.loc[(Data.tempsdg14_04 == "SDG14_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.5

*14.5 By 2020, conserve at least 10 per cent of coastal and marine areas, consistent with national and international law and based on the best available scientific information*

*Innen 2020 bevare minst 10 prosent av kyst- og havområdene, i samsvar med nasjonal rett og folkeretten og på grunnlag av den beste vitenskapelige kunnskapen som er tilgjengelig*



```python
#Termlists
termlist14_5a = ["marine reserve", "ocean reserve", "nature reserve", "marine sanctuar", "marine park", "particularly sensitive sea area", "marine conservation",
                 "nature reserve","national park",
                 "no-take area", "no-take zone", "no-take reserve",

                 "vernområde","vernområde", "vernet økosystem", "marine reservat", "marint vern",
                 "naturreservat", "nasjonalpark", "biotopvernområde", "biosfæreområde", "bevarte område", "bevaringsområde","fredningsområde","nasjonalpark",
                 "fiskeforbud"]
termlist_145acaps = ["MPA","LSMPA","NMTR"] 

termlist14_5b = ["protect","conserved","conservation","conserves","conserving",
                "verne", "verna", "vern av","bevare","bevaring","frede","freda","fredning","beskytt"]

termlist14_5c = ["area","zone", "habitat", "ecosystem",
                "område", "sone", "leveområd", "miljø", "økosystem"]

termlist14_5not = ["landskapsvernområde"]
#This NOT search is needed as this "landskapsvernområde"(NO) is often used for terrestrial conservation, 
# and results are found even with the marine terms because many norwegian place names contain "fjord"...

phrasedefault14_5a = r'(?:{})'.format('|'.join(termlist14_5a))
phrasedefault14_5acaps = r'(?:{})'.format('|'.join(termlist_145acaps))
phrasedefault14_5b = r'(?:{})'.format('|'.join(termlist14_5b))
phrasedefault14_5c = r'(?:{})'.format('|'.join(termlist14_5c))
phrasedefault14_5not = r'(?:{})'.format('|'.join(termlist14_5not))
```


```python
#Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_5a, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasedefault14_5acaps, na=False, case=True)) #case = True
        | ((Data['result_title'].str.contains(phrasedefault14_5b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_5c, na=False, case=False)))
    )
    & (~Data['result_title'].str.contains(phrasedefault14_5not, na=False, case=False))
    & (Data['marine_terms']==True)
),"tempsdg14_05"] = "SDG14_05"

print("Number of results = ", len(Data[(Data.tempsdg14_05 == "SDG14_05")])) 
```


```python
test=Data.loc[(Data.tempsdg14_05 == "SDG14_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.6

*14.6 By 2020, prohibit certain forms of fisheries subsidies which contribute to overcapacity and overfishing, eliminate subsidies that contribute to illegal, unreported and unregulated fishing and refrain from introducing new such subsidies, recognizing that appropriate and effective special and differential treatment for developing and least developed countries should be an integral part of the World Trade Organization fisheries subsidies negotiation*

*Innen 2020 forby visse former for fiskerisubsidier som bidrar til overkapasitet og overfiske, avskaffe subsidier som bidrar til ulovlig, urapportert og uregulert fiske, og dessuten unngå å innføre nye tilsvarende subsidier, samtidig som man erkjenner at en hensiktsmessig og effektiv særskilt og differensiert behandling av utviklingslandene og de minst utviklede landene bør være en integrert del av Verdens handelsorganisasjons forhandlinger om fiskerisubsidier*

Merged phrases 1 and 2.


```python
#Termlists
termlist14_6a = ["subsidy", "subsidies", "subsidiz", "subsidis", 
                 "development assistance", "development aid", "development intervention", "foreign aid", "doha development agenda", "hong kong ministerial", "world trade organization",
                 
                 "subsidier", 
                 "statsstøtte", "offentlig støtte", "utviklingsstøtte", "bistand", "Verdens handelsorganisasjon", "Doha-runden", "ministermøtet i Hongkong"]

termlist14_6acaps = ["ODA", "WTO"]

termlist14_6b = ["fishing", "fisher", "shellfish", "trawl",                
                 "fiske", "skalldyr"]
                #"fishing" will find overfishing

#termlist14_6not = ["larval subsid", "recruitment subsid"] 
#Doesn't seem to be needed here in a title search

phrasedefault14_6a = r'(?:{})'.format('|'.join(termlist14_6a))
phrasespecific14_6acaps = r'\b(?:{})\b'.format('|'.join(termlist14_6acaps))
phrasedefault14_6b = r'(?:{})'.format('|'.join(termlist14_6b))
#phrasedefault14_6not = r'(?:{})'.format('|'.join(termlist14_6not))
```


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault14_6a, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific14_6acaps, na=False, case=True)))
    & (Data['result_title'].str.contains(phrasedefault14_6b, na=False, case=False))
),"tempsdg14_06"] = "SDG14_06"

print("Number of results = ", len(Data[(Data.tempsdg14_06 == "SDG14_06")])) 
```


```python
test=Data.loc[(Data.tempsdg14_06 == "SDG14_06"), ("result_id", "result_title")]
test.iloc[0:10, ]
```

### SDG 14.7

*14.7 By 2030, increase the economic benefits to small island developing States and least developed countries from the sustainable use of marine resources, including through sustainable management of fisheries, aquaculture and tourism*

*Innen 2030 sikre at de økonomiske fordelene ved bærekraftig bruk av havets ressurser, blant annet gjennom bærekraftig forvaltning av fiskeri, akvakultur og turistnæring, i større grad kommer små utviklingsøystater og de minst utviklede landene til gode*


```python
#Termlists
termlist14_7a = ["econom","wealth",
                 "exploit","goods and services","ecosystem service",
                 "marine resource", "biological resource", "genetic resource",
                 "livelihood","job","income","profit","trade","trading","market",
                 "monetary","moneti","investor",
                 "blue growth","blue bond",

                 "økonomi", "rikdom",
                 "marine ressurs", "biologiske ressurs", "biologisk ressurs", "genetiske ressurs", "genetisk ressurs",
                 "utnytt", "varer", "tjenester",
                 "levebrød", "jobb", "arbeid", "inntekt", "handel", "marked", "markad",
                 "penger",
                 "blå vekst", "blåvekst"]
                 #"Blue/Bio economy" and "socioeconomic" (NO: blå/bio økonomi, sosioøkonomisk) is covered by "econom" (NO: økonomi)
                 #"økosystemtjenester" (NO) are covered by "tjenester"

termlist14_7acaps = ["GDP"] #can search case sensitive

termlist14_7b = ["sustainab", "marine conservation",
                 "marine spatial planning",  
                 "ecosystem-based", "ecosystem-based fisheries", "area-based manag", "area-based approach",     
                 "spatial management", "community based management","resilience based management", 
                 "coastal zone management","integrated coastal zone planning","coastal resources management",   
                 "locally managed marine area",
                 "protected area", "marine reserve", "ocean reserve", "nature reserve", "marine park", 
                 "conservation zone", "particularly sensitive sea area",
                 "regional fisheries management",
                 "port state measures agreement",
                 "fish stocks agreement","Management of Straddling Fish Stocks","Management of Highly Migratory Fish Stocks",
                 "code of conduct for responsible fisheries",
                 "Nairobi convention"

                 "bærekraft","berekraft", "marint vern",
                 "økosystem tilnærming", "økosystembasert forvaltning", "økosystembasert styring", "forvaltningsplaner",
                 "integrert kystsone", "kystplanlegging", "kystsoneforvalt",
                 "samfunnsforvalt", "bærekraftig forvalt", "berekraftig forvalt", "arealforvalt",
                 "marint vernområde","marine vernområde","marine verneområde","marine reservat",
                 "naturreservat", "biotopvernområde", "nasjonalpark", 
                 "bevarte område", "bevaringsområde", "fredet område", "vernet område", "marine vernområde", "marine verneområde",
                 #if this term list is used in the search, the agreement translations need to be added from 14.2c here. Currently it is not used (see note below)
                 "fiskeriforvalt", "fiskeriplanlegg", 
                 "likevektsfangst"]

#termlist14_7bcaps = ["LMMA","ICZM","MPA","RFMO","CCRF","UNFSA"] 

phrasedefault14_7a = r'(?:{})'.format('|'.join(termlist14_7a))
phrasedefault14_7acaps = r'(?:{})'.format('|'.join(termlist14_7acaps))
#phrasedefault14_7b = r'(?:{})'.format('|'.join(termlist14_7b))
#phrasedefault14_7bcaps = r'(?:{})'.format('|'.join(termlist14_7bcaps))
```

As this is a title search, we suggest dropping the second element to simplify, so it is enough to mention marine economy in LDCs/SIDS.


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault14_7a, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault14_7acaps, na=False, case=True)))
    #& ((Data['result_title'].str.contains(phrasedefault14_7b, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault14_7bcaps, na=False, case=True)))
    & (Data['LDCSIDS']==True)
    & (Data['marine_terms']==True)
),"tempsdg14_07"] = "SDG14_07"

print("Number of results = ", len(Data[(Data.tempsdg14_07 == "SDG14_07")]))  
```


```python
test=Data.loc[(Data.tempsdg14_07 == "SDG14_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.a

*14.a Increase scientific knowledge, develop research capacity and transfer marine technology, taking into account the Intergovernmental Oceanographic Commission Criteria and Guidelines on the Transfer of Marine Technology, in order to improve ocean health and to enhance the contribution of marine biodiversity to the development of developing countries, in particular small island developing States and least developed countries*

*Styrke vitenskapelig kunnskap, bygge opp forskningskapasitet og overføre marin teknologi – og samtidig ta hensyn til kriterier og retningslinjer fra Den mellomstatlige oseanografiske kommisjon for overføring av marin teknologi – med sikte på å bedre tilstanden i havet og øke det marine artsmangfoldets bidrag til utviklingen i utviklingslandene, særlig i små utviklingsøystater og de minst utviklede landene*

#### Phrase 1


```python
#Termlists
termlist14_aa = ["transfer of marine technolog", "marine technology transfer", "technology transfer",
                 "teknologioverføring", "overføring av marin teknologi", "overføre marin teknologi", "overføre teknologi"]
                 #added "technology transfer" alone, as we are going to search within the marine results anyway

phrasedefault14_aa = r'(?:{})'.format('|'.join(termlist14_aa))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault14_aa, na=False, case=False)) 
    & (Data['marine_terms']==True)
),"tempsdg14_a"] = "SDG14_0a"

print("Number of results = ", len(Data[(Data.tempsdg14_a == "SDG14_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg14_a == "SDG14_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist14_ab = ["establish","build","develop","implement","propos","design","provide","provision",
                 "increas","improv","strengthen","enhanc","upgrad","accelerat","prioriti","promot","enabl",
                 "cooperat","co-operat","collaborat","network","partnership",
                 "open data","data sharing","open science",
                 "technology transfer", "knowledge transfer", "technical transfer",
                 "invest", "fund", "financ", "grant", "support", "assist",
                 "international network",
                 "policy","policies","initiativ","framework","governance","strateg","program","agenda",
                 "innovation",

                 "etablere","bygg","utvikl","tilbyr",
                 "forbedr","styrk","bedring", "betring","oppgrad","muliggjør",
                 "samarbeid","nettverk","partnerskap",
                 "åpne data","datadeling","åpen tilgang","åpen vitenskap","åpen forskning",
                 "teknologioverføring","kunnskapsoverfør", "tekniskoverfør",
                 "finansiering", "forskningsmidler", "støtte",
                 "internasjonalt nettverk","internasjonale nettverk",
                 "politikk", "retningslinj", "rammeverk", "styring", "ledelse", "leiing",
                 "innovasjon"] 
                 #several words work in both languages (e.g. "promot", "design", "assist", "strateg")            
                 
termlist14_ac = ["plan","planned","planning","aid","ODA",
                 "øke", "øker", "midler"] #Control truncation

termlist14_ad = ["knowledge","technolog","technical","research","scientific","R&D",
                 "kunnskap", "teknologi", "teknisk", "forskning", "vitenskap", "innovasjon"]
termlist14_ae = ["sharing","shared","share","cooperat","co-operat","collaborat","partnership","network",
                 "deling", "samarbeid", "partnerskap", "nettverk"]

termlist14_af = ["research", "science", "scientific", "biotech", "ocean technolog",
                 "data infrastructure","data network","big data","smart ocean","modelling technique",
                 "biomonitoring","remote sensing equipment","tide gauge",

                 "forskning", "vitenskap", "bioteknol", "havteknolog", "marin teknolog",
                 "data infrastruktur", "datanettverk", "stordata", "smart hav", "modellering",
                 "miljøovervåk", "miljøovervak", "fjernmålingsutstyr"]
                 #Originally, some of these terms were combined with the terms in termlist14_aj, but in a title search we felt they worked alone.

termlist14_ag = ["observation","observator","monitoring","equipment",
                 "observasjon", "overvåk", "overvak", "utstyr"]
termlist14_ah = ["ocean","marine","biolog","ecological","ecological","environmental","network","facilit","system",
                 "hav", "sjø", "marin", "økologi", "miljø", "nettverk", "fasilitet", "system"]
                 
termlist14_ai = ["taxonom","genetic","species","diversit","technolog", "technical",
                 "taksonom", "genetisk", " art", "teknolog", "teknisk"]
termlist14_aj = ["knowledge","capacity","advisor","capabilit","training","expertise","skills","compentenc",
                 "infrastructure","facilities","research vessel","vehicle","laborator","equipment","herbari","museum collection",
                 "software"," data","register","reference librar","inventory","inventories","information system",
                 "guideline",
                 "investment","funding","GERD","expenditure",
                 "network","sharing","joint research","joint effort","collaborat","international cooperation",

                 "kunnskap", "kapasitet", "rådgi", " evne", "opplær", "ekspert", "ferdighet", "kompetanse",
                 "infrastruktur", "fasilitet", "forskningsskip", "forskningsfartøy", "utstyr", "museum samling",
                 "programvare", "forskningsdata", "inventar", "datasystem", 
                 "retningslinj",
                 "midler", "pengebruk", "utgift",
                 "nettverk", "deling", "samarbeid"]

termlist14_anot = ["torp sandefjord"]
#There are a lot of reports about torp sandefjord which show up due to "Fjord"- manually removed them here (Norway only)

phrasedefault14_ab = r'(?:{})'.format('|'.join(termlist14_ab))
phrasespecific14_ac = r'\b(?:{})\b'.format('|'.join(termlist14_ac))
phrasedefault14_ad = r'(?:{})'.format('|'.join(termlist14_ad))
phrasedefault14_ae = r'(?:{})'.format('|'.join(termlist14_ae))
phrasedefault14_af = r'(?:{})'.format('|'.join(termlist14_af))
phrasedefault14_ag = r'(?:{})'.format('|'.join(termlist14_ag))
phrasedefault14_ah = r'(?:{})'.format('|'.join(termlist14_ah))
phrasedefault14_ai = r'(?:{})'.format('|'.join(termlist14_ai))
phrasedefault14_aj = r'(?:{})'.format('|'.join(termlist14_aj))
phrasedefault14_anot = r'(?:{})'.format('|'.join(termlist14_anot))
```


```python
#Search 1
Data.loc[(
    ( (Data['result_title'].str.contains(phrasedefault14_ab, na=False, case=False)) 
    | (Data['result_title'].str.contains(phrasespecific14_ac, na=False, case=False))
    | ((Data['result_title'].str.contains(phrasedefault14_ad, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_ae, na=False, case=False)))
    )
    &  
    ( (Data['result_title'].str.contains(phrasedefault14_af, na=False, case=False)) 
    | ((Data['result_title'].str.contains(phrasedefault14_ag, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_ah, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasedefault14_ai, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_aj, na=False, case=False)))
    )
    & (~Data['result_title'].str.contains(phrasedefault14_anot, na=False, case=False))
    & (Data['marine_terms']==True)
),"tempsdg14_a"] = "SDG14_0a"

print("Number of results = ", len(Data[(Data.tempsdg14_a == "SDG14_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg14_a == "SDG14_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist14_ak = ["blue growth","blue econom","marine economy",
                 "blå vekst", "blåvekst", "blå økonomi", "marin økonomi"]                   
termlist14_al = ["sustainab",
                 "bærekraft", "berekraft"] 

termlist14_am = ["bioresource","biological resource","genetic resource","living marine resources",
                 "biodivers","biological diversity","BBNJ","species diversity","genetic diversity","genomic diversity","taxonomic diversity",

                 "bioressurs", "biologiske ressurs", "genressurs", "genetiske ressurs", "levende marine ressurs",
                 "biologisk diversit", "biologisk mangf", "artsmangf", "genetisk mangf", "taksonomisk mang", "naturmangf"]

termlist14_an = ["bioprospect","biopiracy","Nagoya","biotech","marine natural product","bioactive",
                 "bio-econom","bioeconom","blue growth","blue econom","blue bond","marine economy",
                 "benefit","sustainable development","development intervention","human development","social development","economic development",
                 "tourism","tourist","sightsee",
                 "fisher","fishing","aquaculture","mariculture","fish farm","harvest","aquarium trade",
                 "exploit","goods and services","ecosystem service",
                 "social ecological","socialecological","socioecological","socio economic","socioeconomic",
                 "econom","GDP","wealth","monetary","moneti","investor",
                 "livelihood","job","income","profit",
                 "trade","trading","market",
                 "sustainable use", "use sustainab", "using sustainab", "sustainable usage",

                 "biopirat", "bioteknolog", "bioaktiv",
                 "bioøkonom", "blå vekst", "blå økonomi", "blå aksjer", "marin økonomi",
                 "fordel", "gevinst", "bærekraftig utvik", "berekraftig utvik", "bistand", "menneskelig utvikling", "økonomisk utvikling", "levekårsutvikling", "sosial utvikling",
                 "turism", "turist", 
                 "fiske", "akvakultur", "havbruk", "akvarie",
                 "utnytt", "varer og tjeneste", "økosystem tjenest",
                 "sosio-økologisk", "sosioøkologi", "sosioøkonomisk", "sosio-økonomisk",
                 "økonomi", "BNP", "rikdom", "penger", "investor",
                 "levebrød", "arbeid", "inntekt", "avkastn",
                 "handel", "marked",
                 "bærekraftig bruk", "berekraftig bruk",  "selvbærende", "sjølvberande", "miljøvennlig", "miljøvennleg", "miljøvenleg", "miljøbevisst"]

phrasedefault14_ak = r'(?:{})'.format('|'.join(termlist14_ak))
phrasedefault14_al = r'(?:{})'.format('|'.join(termlist14_al))
phrasedefault14_am = r'(?:{})'.format('|'.join(termlist14_am))
phrasedefault14_an = r'(?:{})'.format('|'.join(termlist14_an))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_ak, na=False, case=False)) #& (Data['result_title'].str.contains(phrasedefault14_al, na=False, case=False)))
        | ((Data['result_title'].str.contains(phrasedefault14_an, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_am, na=False, case=False)))  
    )
    & (Data['LMICs']==True)
    & (Data['marine_terms']==True)
),"tempsdg14_a"] = "SDG14_0a"

print("Number of results = ", len(Data[(Data.tempsdg14_a == "SDG14_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg14_a == "SDG14_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.b
*14.b Provide access for small-scale artisanal fishers to marine resources and markets*

*Gi fiskere som driver småskala fiske, tilgang til marine ressurser og markeder*

Phrase 1 and 2 merged.


```python
#Termlists
termlist14_ba = ["access", "right",
                 "commons", "common property", "common fishing", "ownership", "inheritance",
                 "conflict", "dispute", "contested", "competition",
                 "inequit", "marginali", "criminal", "appropriat",
                 "blue injustice", "blue justice", "distributional justice",
                 "governance", "planning" , "legislation" , "policy" , "policies" , "framework" , "strateg" , "legislat" , "regulations",

                 "tilgang", "rett",
                 "felles", "eierskap",
                 "konflikt", "tvist", "konkurrans",
                 "kriminel", "stjel",
                 "styring", "ledelse", "leiing", "politikk", "retningslinj", "rammverk", "planlegging", "regulativ", "lovgiv", "forskrift",]
                #"rett"(NO) covers both rights and justice (rett, rettferd)

termlist14_bb = ["law", "laws",
                 "lov", "lovverk", "arv"] #terms to control truncation

termlist14_bc = ["fishing", "fisher", "fish market", "shellfish", "marine resource", "marine harvest",                
                 "fiske", "skalldyr", "marine ressurs", "havbruk"]

termlist14_bd = ["traditional fishing","small-scale", "artisan", "subsistence", "indigenous", "sami", "sapmi", 
                 "tradisjonel", "småskala", "subsistens", "levebrød", "urfolk", "urbefolk", "samene"]

phrasedefault14_ba = r'(?:{})'.format('|'.join(termlist14_ba))
phrasespecific4_bb = r'\b(?:{})\b'.format('|'.join(termlist14_bb))
phrasedefault14_bc = r'(?:{})'.format('|'.join(termlist14_bc))
phrasedefault14_bd = r'(?:{})'.format('|'.join(termlist14_bd))
```


```python
#Search 1

Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault14_ba, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_bb, na=False, case=False)))
    & 
    (
        (Data['result_title'].str.contains(phrasedefault14_bc, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault14_bd, na=False, case=False))
    )
),"tempsdg14_b"] = "SDG14_b"

print("Number of results = ", len(Data[(Data.tempsdg14_b == "SDG14_b")]))  
```


```python
test=Data.loc[(Data.tempsdg14_b == "SDG14_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.c

*14.c Enhance the conservation and sustainable use of oceans and their resources by implementing international law as reflected in the United Nations Convention on the Law of the Sea, which provides the legal framework for the conservation and sustainable use of oceans and their resources, as recalled in paragraph 158 of “The future we want”*

*Styrke bevaring og bærekraftig bruk av havene og de marine ressursene ved å implementere folkeretten slik den er reflektert i FNs havrettskonvensjon, som utgjør rettsgrunnlaget for bevaring og bærekraftig bruk av havene og de marine ressursene, slik det framgår av punkt 158 i FN-rapporten «The Future We Want»*


#### Phrase 1 & 2

A website with Norwegian and English names for international environmental agreements from the Norwegian Environment Agency was used to help translate agreement names (https://www.miljodirektoratet.no/regelverk/konvensjoner/; accessed 24/01/23)


```python
#Termlists
termlist14_ca = ["law of the sea",
                 "diversity beyond national jurisdiction", "high seas treaty",
                 "common fisheries policy",
                 "marine stewardship council",
                 "regional fisheries management organi",
                 "fish stocks agreement",
                 "code of conduct for responsible fisheries",
                 "port state measures agreement",
                 "Management of Straddling Fish Stocks","Management of Highly Migratory Fish Stocks",
                 "deep-sea fisheries guidelines","Management of Deep-sea Fisheries in the High Seas",
                 "North Atlantic Salmon conservation Organization",
                 "marine spatial planning directive",
                 "Regional seas programme",
                 "Marine strategy framework directive",
                 "OSPAR convention","Convention for Protection of the Marine Environment of the North-East Atlantic",
                 "Barcelona convention",
                 "Global Programme of Action for the Protection of the Marine Environment",
                 "prevention of pollution from ships",
                 "Conservation of Antarctic Living Marine Resources", "Agreement on the Conservation of Polar Bears",

                 "havrettskonvensjon","Havrettstraktaten", "havtraktat",
                 "avtalen om verdenshavene",
                 "felles fiskeripolitik",
                 "avtalen om fiske på det åpne hav",
                 "avtalen om havnestatstiltak",
                 "avtalen om fiske på vandrende bestander",
                 "regulering av fisket etter dyphavsarter",
                 "Den nordatlantiske laksevernorganisasjonen",
                 "havstrategidirektiv", 
                 "Konvensjonen for bevaring av det marine miljø", "Oslo-Paris-konvensjonen", 
                 "Isbjørnavtalen"]
                #Terms that can be searched for in all data, are about marine law/agreements

termlist14_ca_case = ["UNCLOS","ABNJ","BBNJ","RFMO","CCRF","UNFSA","MSFD","MARPOL"] #terms to use uppercase

termlist14_cb = ["the future we want",
                 "habitats directive","convention on biological diversity",
                 "Convention on International Trade in Endangered Species",
                 "World Heritage Convention",
                 "Water framework directive",
                 "Bern convention", "Convention on the Conservation of European Wildlife and Natural Habitats",
                 "Bonn convention","Convention on the Conservation of Migratory Species of Wild Animals",
                 "stockholm convention",

                 "habitatdirektiv", "Konvensjon om biologisk mangfold", "Konvensjonen om biologisk mangfold", "biodiversitetskonvensjon",
                 "Konvensjonen om internasjonal handel med truede dyr","internasjonal handel med truede og sårbare arter",
                 "verdensarvkonvensjonen",
                 "Vannrammedirektiv",
                 "Bernkonvensjonen", "Bern-konvensjon", "Konvensjonen om vern av ville europeiske planter og dyr",
                 "Bonnkonvensjonen", "Bonn-konvensjon", "konvensjonen om bevaring av trekkende ville dyr",
                 "Stockholmkonvensjonen", "Stockholm-konvensjon"]
                #Terms that need to be used with marine terms

phrasedefault14_ca = r'(?:{})'.format('|'.join(termlist14_ca))
phrasedefault14_ca_case = r'(?:{})'.format('|'.join(termlist14_ca_case))
phrasedefault14_cb = r'(?:{})'.format('|'.join(termlist14_cb))
```


```python
#Search in marine set for generic environmental legislation, and in the whole data for marine specific legislation
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault14_ca, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault14_ca_case, na=False, case=True)))
    |((Data['result_title'].str.contains(phrasedefault14_cb, na=False, case=False)) & (Data['marine_terms']==True))
),"tempsdg14_c"] = "SDG14_c"

print("Number of results = ", len(Data[(Data.tempsdg14_c == "SDG14_c")])) 
```


```python
test=Data.loc[(Data.tempsdg14_c == "SDG14_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist14_cc = ["international", "beyond national jurisdiction", "high seas", "europ", "pacific", "asia", "africa", "latin america", "south america", "arctic",
                 "internasjonal", "stillehavet", "afrika", "sør-amerika", "arktisk"]

termlist14_cccaps = ["UN", "ABNJ",
                     "FN"]

termlist14_cd = ["governance","policy","policies","regulat","legal","legislat","agreement","treaty","treaties","framework","instrument",
                 "styring", "ledelse", "leiing", "politikk", "retningslin", "rammeverk", "styring", "planlegging", "regulativ", "lovgivning", "rett", "juridisk", "lovverk", "forskrift"]

termlist14_ce = ["law", "laws"
                 "lov"] #terms to limit truncation

termlist14_cf = ["conservation","sustainab","ecosystem restoration",
                 "ecosystem based management","area based management","resilience based management",
                 "coastal zone management","integrated coastal zone planning","coastal resources management",
                 "community based management","locally managed marine area$",
                 "marine spatial planning","spatial management",
                 "herbivore management area","ecosystem approach",
                 "protected area", "marine reserve","ocean reserve","marine park","marine sancturary",
                 "nature reserve","conservation zone","particularly sensitive sea area",
                 "biodivers", "biological diversity",
                 "blue growth","blue econom",

                 "forvalt", "vernet", "miljøvern", "bevart", "bevaring", "fredet", "fredning", "gjenoppbygg", "restaurer", "bærekraft",
                 "økosystembasert forvaltning", "økosystembasert styring", "forvaltningsplaner",
                 "samfunnsforvalt", "bærekraftig forvalt", "berekraftig forvalt", "arealforvaltning",
                 "integrert kystsone", "kystplanlegging", "kystsoneforvaltning",
                 "marint vernområde","marine vernområde","marine verneområde","marine reservat",
                 "naturreservat", "biotopvernområde", "nasjonalpark", "bevarte område",
                 "biologisk diversit","biologisk mangfold",
                 "blåvekst", "blå vekst", "blå økonomi"]

termlist14_cfcaps = ["MSP", "ICZM", "LMMA", "MPA", "LSMPA"] #terms to search case sensitive

phrasedefault14_cc = r'(?:{})'.format('|'.join(termlist14_cc))
phrasespecific14_cccaps = r'\b(?:{})\b'.format('|'.join(termlist14_cccaps))
phrasedefault14_cd = r'(?:{})'.format('|'.join(termlist14_cd))
phrasespecific14_ce = r'\b(?:{})\b'.format('|'.join(termlist14_ce))
phrasedefault14_cf = r'(?:{})'.format('|'.join(termlist14_cf))
phrasedefault14_cfcaps = r'(?:{})'.format('|'.join(termlist14_cfcaps))

```


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault14_cc, na=False, case=False))  | (Data['result_title'].str.contains(phrasespecific14_cccaps, na=False, case=False)) )
    & ((Data['result_title'].str.contains(phrasedefault14_cd, na=False, case=False))  | (Data['result_title'].str.contains(phrasespecific14_ce, na=False, case=False)) )
    & ((Data['result_title'].str.contains(phrasedefault14_cf, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault14_cfcaps, na=False, case=True)) )
    & (Data['marine_terms']==True)
),"tempsdg14_c"] = "SDG14_c"

print("Number of results = ", len(Data[(Data.tempsdg14_c == "SDG14_c")])) 
```


```python
test=Data.loc[(Data.tempsdg14_c == "SDG14_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14 mentions

Works mentioning SDG14

Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 

"SDG" was also not searched for case-sensitive, as it seems to work ok without.


```python
#Termlists

termlist_sdg_a = ["SDG 14", "SDGs 14", "SDG14", "sustainable development goal 14", 
                  "bærekraftsmål 14", "berekraftsmål 14"]
termlist_sdg_b = ["sustainable development goal", 
                  "bærekraftsmål", "berekraftsmål"]
termlist_sdg_c = ["goal 14",
                  "mål 14"]
termlist_sdg_d = ["sustainable development goal", "SDG", "goal 14", 
                  "bærekraftsmål", "berekraftsmål", "mål 14"]
termlist_sdg_e = ["ocean.*", "marine", "sea", "seas", "fisher.*",
                  "hav", "havet", "sjø", "marin", "fisker.*"]

termlist_sdg_f = ["life below water", "livet i havet", "Liv under vatn"]
#extra phrase where the short titles of the SDG are included, since this is a title search

phrasedefault_sdg_a = r'(?:{})'.format('|'.join(termlist_sdg_a))
phrasedefault_sdg_b = r'(?:{})'.format('|'.join(termlist_sdg_b))
phrasedefault_sdg_c = r'(?:{})'.format('|'.join(termlist_sdg_c))
phrasedefault_sdg_d = r'(?:{})'.format('|'.join(termlist_sdg_d))
phrasespecific_sdg_e = r'\b(?:{})\b'.format('|'.join(termlist_sdg_e))
phrasedefault_sdg_f = r'(?:{})'.format('|'.join(termlist_sdg_f))
```


```python
#Search 1
Data.loc[(
      (Data['result_title'].str.contains(phrasedefault_sdg_a, na=False, case=False))
      |(Data['result_title'].str.contains(phrasedefault_sdg_f, na=False, case=False))
      |((Data['result_title'].str.contains(phrasedefault_sdg_b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault_sdg_c, na=False, case=False)))
      |((Data['result_title'].str.contains(phrasedefault_sdg_d, na=False, case=False)) & (Data['result_title'].str.contains(phrasespecific_sdg_e, na=False, case=False)))
),"tempmentionsdg14"] = "SDG14"
    
print("Number of results = ", len(Data[(Data.tempmentionsdg14 == "SDG14")]))
```


```python
test=Data.loc[(Data.tempmentionsdg14 == "SDG14"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 15

Webpages about SDG targets from the UN Association of Norway were used to get target translations and to help with Norwegian terms (https://www.fn.no/om-fn/fns-baerekraftsmaal/livet-paa-land).

Have also used "Realfagstermer", a controlled vocabulary for scientific terms from the University of Oslo and University of Bergen - https://app.uio.no/ub/emnesok/realfagstermer/search

Natur i Norge (Artsdatabanken) was used to help with translation of terrestrial and limnic habitats - https://www.artsdatabanken.no/NiN/Natursystem/Typeinndeling (accessed 24/01/23

A website with Norwegian and English names for international environmental agreements from the Norwegian Environment Agency was used to help translate agreement names - https://www.miljodirektoratet.no/regelverk/konvensjoner/ (accessed 24/01/23)

### Terrestrial terms
Used together with most (but not all) targets to try and limit the results to the terrestrial/limnic environment. Done by creating a T/F column that can be combined with other searches. There are two variants - an AND set, and a double NOT set, that are used variously as needed. The double NOT variant is used because many terrestrial works may not indicate habitat type. 

* terr_terms : T = contains a word indicating it is about the terrestrial/limnic environment. 
* terrestrial_double_NOT : T = does not contain marine terms alone (e.g. a title talking about coral and peatlands will be included, but one only about coral will not). 


```python
## The terrestial list
#---------------------------------

termlist15_terr1 = ["terrestrial",
                    "forest", "woodland", "taiga", "jungle", "mangrove", 
                    "peatland", "peat land", "swamp", "wetland", "marsh", "paludal",
                    "farmland", "agricultural land", "cropland", "pasture", "rangeland",
                    "shrub", "meadow", "bushland", "heath", "moorland",
                    "savanna","grassland","prairie",
                    "dryland", "dry land", "desert", 
                    "lowland",
                    "mountain", "highland", "alpine", "tundra", "upland",
                    "freshwater", "limnic", "inland fish",
                    "brook", "creek",

                    "terrestrisk", "landlevende", "villmarksområd",
                    "skog", "jungel",
                    "torv", "torvmos", "torvmyr", "slåttemyr", "myrer", "myrar", "sumper", "sumpar", "våtmark", "våteng", "torvmark",
                    "dyrket mark", "dyrket jord", "dyrka jord", "dyrka mark", "landbruksmark", "utmark", "innmark", "beite",
                    "kratt", "busker", "lynghei",
                    "engmark", "natureng", "kultureng", "engvegeta", "moseeng", "gresseng", "strandeng", "slåttemark", 
                    "prærie", "tørre område",
                    "tørrmark", "ørken", "halvtørre områd",
                    "fjell", "bergtopp", "alpin", 
                    "ferskvann", "ferskvatn", "innlandsfisk", "innsjø"]

termlist15_terr2 = ["soil", "soils", "bog", "bogs", "mire", "mires", "fen", "fens", "bush", "bushes", "plains", "steppe",
                    "lake", "lakes", "pond", "ponds", "river", "rivers", "stream", "streams",

                    "jord", "åker", "myr", "sump", "eng", "enger", "busk", "elv", "elver", "bekk"]

phrasedefault15_terr1 = r'(?:{})'.format('|'.join(termlist15_terr1))
phrasespecific15_terr2 = r'\b(?:{})\b'.format('|'.join(termlist15_terr2))
```


```python
Data["terr_terms"] = (
    (Data['result_title'].str.contains(phrasedefault15_terr1, na=False, case=False))
    | (Data['result_title'].str.contains(phrasespecific15_terr2, na=False, case=False))
)

len(Data.loc[Data['terr_terms']])
```


```python
#Results
test=Data.loc[Data['terr_terms']]
test.iloc[0:10, [0,4,5,6,8]]
```


```python
## The terrestial double NOT list
#---------------------------------

termlist_noise = ["marin", "coral", "ocean", "seafloor", "deep-sea", "deep sea","kelp", 
                  "random forest", "internet of thing", "urban ecosystem",
                  "salivary microbio","gut microbio","skin microbio","oral microbiome","gut flora","skin flora","immunologi","immunology","hormon","syndrome","vector","enzyme","infected","infection","infect",
                  
                  "korall", "sjøbunn", "sjøbotn", "havbunn", "havbotn", "havdyp", "havdjup", "dyphav", "djuphav", "tareskog", "tare skog",
                  "språk", "barnevernet"]
                  #"språk" (NO: language) is added here as in Norwegian a lot of the same terms are used for language conservation as nature conservation (e.g. forvaltningsområde).
                  #"barnevernet" (NO: child protective services) also
                  #The medical terms (line 3) are from 15.1 phrase 3. We have included all from the WOS string except from parasite.

termlist_noise2 = ["IOT", "hav", "havet"]
phrasedefault_noise = r'(?:{})'.format('|'.join(termlist_noise))
phrasespecific_noise_2 = r'\b(?:{})\b'.format('|'.join(termlist_noise2))
```


```python
mask15_pre = Data.loc[(Data['result_title'].str.contains(phrasedefault_noise, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific_noise_2, na=False, case=False))]
#Select all that include marine terms

mask15 = mask15_pre.loc[~((mask15_pre['result_title'].str.contains(phrasedefault15_terr1, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_terr2, na=False, case=False)))]
#Select those that don't also include one of the terrestrial terms - i.e. they are purely marine
#Note that this will not successfully remove "kelp forest" (/tareskog) as these contain the terms forest(/skog).

print("Number of results = ", len(Data)) 
```


```python
Data["terrestrial_double_NOT"] = (~Data.index.isin(mask15.index))

print("Number of original results = ", len(Data)) 
print("Number of double NOT results = ",(len(Data.loc[Data['terrestrial_double_NOT']])))
print("Number of results dropped = ",((len(Data.loc[Data['terrestrial_double_NOT']]))-(len(Data))))
```


```python
#Results
test=Data.loc[Data['terrestrial_double_NOT']]
test.iloc[15:25, [0,4,5,6,8]]
```

### SDG 15.1

*15.1 By 2020, ensure the conservation, restoration and sustainable use of terrestrial and inland freshwater ecosystems and their services, in particular forests, wetlands, mountains and drylands, in line with obligations under international agreements*

*Innen 2020 bevare og gjenopprette bærekraftig bruk av ferskvannsbaserte økosystemer og tjenester som benytter seg av disse økosystemene, på land og i innlandsområder, særlig skoger, våtmarker, fjell og tørre områder, i samsvar med forpliktelser i internasjonale avtaler.*


#### Phrase 1


```python
#Termlists
termlist15_1a = ["protected area","conservation area","conservation zone","Wilderness area","Nature reserve","National park",
                 "Habitat management area","Species management area","Protected landscape",
                 "conserved ecosystem","conservation ecosystem", "protected ecosystem","protecting ecosystem", "protect ecosystem",

                 "vernområde","bevarte område", "bevaringsområde", "naturreservat","biotopvernområde","biosfæreområde","nasjonalpark",
                 "landskapsvern","økosystemforvalt","økosystembasert forvalt",
                 "vernet økosystem","fredningsområde","forvaltningsområde"]

termlist15_1b = ["protect", "preserv", "conserv", "reforest", "re-forest", "rehabilit", "restor",
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer", "skogplanting", "gjengro"]
                 #"vernet" (NO) will also find "vernetiltak"
    
termlist15_1c = ["habitat","biotop", 
                 "leveområd"]

phrasedefault15_1a = r'(?:{})'.format('|'.join(termlist15_1a))
phrasedefault15_1b = r'(?:{})'.format('|'.join(termlist15_1b))
phrasedefault15_1c = r'(?:{})'.format('|'.join(termlist15_1c))
```


```python
#Search in terr double NOT

Data.loc[(
    (    
        (Data['result_title'].str.contains(phrasedefault15_1a, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault15_1b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault15_1c, na=False, case=False)))
    )
    &(Data['terrestrial_double_NOT']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
test=Data.loc[(Data.tempsdg15_01 == "SDG15_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist15_1d = ["protect","preserv","conserv", "reforest", "re-forest", "rehabilit", "restor",
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer", "skogplanting", "gjengro"]
                 #"vernet"(NO) will also find "vernetiltak"
    
termlist15_1e = ["ecosystem", "ecolog", "zone", "environment", "protected area", "protected zone", "protection zone", "conservation area", "conservation zone",
                 "økosystem", "kulturlandskap", "landskapsvern", "miljøvern", "miljøparagraf"]
#Supplement with the terrestrial terms in phrasedefault15_terr1 and phrasedefault15_terr2
#Added "natur" and "kulturlandskap"(NO) instead of "område"(NO) because there were too many results from cultural/human conservation
#"landskap"(NO) alone got a lot of cultural results, so it is combined to specific types
#"area" is also combined, as this solution works well to cut away 95 % noisy results

termlist15_1etrunc = ["natur"] #prevent left truncation (e.g. signatur)

phrasedefault15_1d = r'(?:{})'.format('|'.join(termlist15_1d))
phrasedefault15_1e = r'(?:{})'.format('|'.join(termlist15_1e))
phrasespecific15_1etrunc = r'\b(?:{})'.format('|'.join(termlist15_1etrunc))
```


```python
#Search 1 - in terr double NOT

Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_1d, na=False, case=False))
        & ((Data['result_title'].str.contains(phrasedefault15_1e, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific15_1etrunc, na=False, case=False)))
        & (Data['terrestrial_double_NOT']==True)
    )
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
#Search 2 - in terr
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_1d, na=False, case=False))
    & (Data['terr_terms']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
test=Data.loc[(Data.tempsdg15_01 == "SDG15_01"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

#### Phrase 3


```python
#Termlists
termlist15_1f = ["protect","preserv","conserv","restore", "restoring", "restoration", "sustainable",
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer", "bærekraft", "berekraft"]
                 #"vernet"(NO) will also find "vernetiltak"
    
termlist15_1g = ["habitat", "nature conservation",
                 "biodivers","biological diversity","species diversity","functional diversity","genetic diversity","taxonomic diversity",
                 "key species","keystone species","foundation species","habitat forming species","key resource",
                 
                 "leveområd", "naturvern",
                 "biologisk mangf", "biomangf", "biologiske mangf", "artsmangf", "artsdiversitet", "naturmangf", "genetisk mangf", "genetisk diversitet",
                 "nøkkelart"]

termlist15_1h = ["diversity", "community", "ecosystem",
                 "diversitet", "mangfold", "mangfald", "samfunn", "økosystem"]
termlist15_1i = ["ecolog", "taxonomic", "species", "plant", "animal", "organism", "flora", "fauna", "insect", "amphibian","reptil", "bird", "mosses", "tree", "grassland", "pollinator",
                 "taksonomisk", "økolog", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl", "moser", "mosar", "trær"] 
                 #"dyr" (NO:animal) is difficult in Norwegian as it is a part of many non-relevant words, but also relevant words, so is difficult to control with truncation. Added in combinations.

phrasedefault15_1f = r'(?:{})'.format('|'.join(termlist15_1f))
phrasedefault15_1g = r'(?:{})'.format('|'.join(termlist15_1g))
phrasedefault15_1h = r'(?:{})'.format('|'.join(termlist15_1h))
phrasedefault15_1i = r'(?:{})'.format('|'.join(termlist15_1i))
```


```python
#Search 1 in double NOT
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_1f, na=False, case=False))
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_1g, na=False, case=False))
            | ((Data['result_title'].str.contains(phrasedefault15_1h, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault15_1i, na=False, case=False)))
        )
    & (Data['terrestrial_double_NOT']==True)
    )
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 


#Search 2 - in terrestrial
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_1f, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault15_1h, na=False, case=False))
    & (Data['terr_terms']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
test=Data.loc[(Data.tempsdg15_01 == "SDG15_01"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

#### Phrase 4

Note that here one can expect some marine results regarding fishing - this is because relatively many fishing works concern fisheries management generally, and trying to limit to either marine or freshwater is very challenging. 


```python
#Termlists
termlist15_1j = ["agro-ecological","agro ecological",
                 "key biodiversity area", "important sites for biodiversity",
                 "ecotourism","eco-tourism",
                 
                 "nøkkelhabitat","nøkkelbiotop",
                 "økoturis", "øko-turis"]

termlist15_1k = ["sustainabl", "responsibl", "environmental", "ecological", "ecosystem approach",
                 "bærekraft", "berekraft", "ansvarlig", "ansvarleg", "miljø", "økologisk", "økosystemtilnærm", "økosystembasert forvaltning"]

termlist15_1l = ["grazing", "forestry", "fishing", "fisher", "hunter", "hunting", "trapping",
                 "beite", "skogbruk", "ferskvannsfisk", "innlandsfisk", "ferskvannskreps", "laks", "ørret", "auret", "jakt", "fangst"]
                 #Fishing terms in Norwegian are limited to freshwater since there is so much marine research. 
                  #44 results dropped, nearly all marine, should be found by SDG14. Salmon and trout included as partially freshwater.

termlist15_1m = ["long term management", "long-term management", 
                 "langsiktig miljøforvaltning", "langsiktig forvalt"]

termlist15_1n = ["manag", "sustainable us", "responsible us", "usage", "development", "ecosystem approach",
                 "govern", "administr", "planning", "policies", "policy", "strateg",
                 "recreation", "tourism", "tourist",
                 "fuel wood", "fire wood", "firewood",
                 
                 "forvalt", "bruk", "bruker", "økosystemtilnærm", "økosystembasert forvaltning",
                 "planlegg", "styring", "ledelse", "leiing", "politikk", 
                 "fritid", "tursti", "turist", "turism", 
                 "fyringsved", "bjørkeved"] 
#"ved" (NO: firewood) is difficult in Norwegian because it is often combined with other words (can't stop truncation), AND is a preposition (ved also = "by")

termlist15_1o = ["ecosystem service","natural resource","groundwater",
                 "biodiversit","biological diversity",
                 "fishing", "hunting", "trapping",
                 
                 "økosystemtjenest", "ferskvann", "ferskvatn",
                 "biologisk diversitet", "biologisk mangf", "biologiske mangf", "biomangf", "artsmangf",
                 "ferskvannsfiske", "innlandsfiske", "laksefiske", "ørretfiske", "auretfiske", "jakt", "fangst"]

phrasedefault15_1j = r'(?:{})'.format('|'.join(termlist15_1j))
phrasedefault15_1k = r'(?:{})'.format('|'.join(termlist15_1k))
phrasedefault15_1l = r'(?:{})'.format('|'.join(termlist15_1l))
phrasedefault15_1m = r'(?:{})'.format('|'.join(termlist15_1m))
phrasedefault15_1n = r'(?:{})'.format('|'.join(termlist15_1n))
phrasedefault15_1o = r'(?:{})'.format('|'.join(termlist15_1o))
```


```python
#Search 1 - in double NOT
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_1j, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault15_1k, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault15_1l, na=False, case=False)))
        | ((Data['result_title'].str.contains(phrasedefault15_1m, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault15_1o, na=False, case=False)))
        |
        (
            (Data['result_title'].str.contains(phrasedefault15_1k, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault15_1n, na=False, case=False))   
            & (Data['result_title'].str.contains(phrasedefault15_1o, na=False, case=False))
        )
    )
    &(Data['terrestrial_double_NOT']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 


#Search 2 - in terrestrial terms
Data.loc[(  
    (
        (Data['result_title'].str.contains(phrasedefault15_1m, na=False, case=False))
        | (Data['result_title'].str.contains(phrasedefault15_1k, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault15_1n, na=False, case=False))   
    )
    & (Data['terr_terms']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
test=Data.loc[(Data.tempsdg15_01 == "SDG15_01"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

#### Phrase 5


```python
#Termlists
termlist15_1s = ["Convention on Biological Diversity",
                 "Convention to Combat Desertification",
                 "Convention on International Trade in Endangered Species of Wild Fauna and Flora",
                 "Nagoya","Plant Genetic Resources for Food and Agriculture","International Seed Treaty","Plant Treaty",
                 "Convention on Wetlands of International Importance", "Ramsar convention",
                 "Bonn convention", "Convention on the Conservation of Migratory Species of Wild Animals",

                 "Konvensjon om biologisk mangfold", "Konvensjonen om biologisk mangfold", "biodiversitetskonvensjon",
                 "Naturmangfoldloven", "lov om vern av naturens mangfold",
                 "Konvensjonen om internasjonal handel med truede dyr", "handel med truede og sårbare arter",
                 "Den internasjonale plantetraktaten",
                 "Ramsarkonvensjon", "Ramsar-konvensjon", "Våtmarkskonvensjonen",
                 "Bonnkonvensjon", "Bonn-konvensjon", "konvensjonen om bevaring av trekkende ville dyr"]
termlist15_1tcase = ["UNCCD", "CITES", "ITPGRFA"]      

termlist15_1u = ["Framework Convention on Climate Change", "UNFCCC", "CBD",
                 "world heritage convention",
                 "European landscape convention",

                 "Klimakonvensjon.*", "rammekonvensjon om klimaendring.*",
                 "verdensarvkonvensjon.*",
                 "landskapskonvensjon.*"]       

termlist15_1v = ["ecosystem", "habitat", "environment", "biotop", "ecolog", "species", "plant", "animal", "organism", "flora", "fauna", "biodivers", "biological diversit",
                 "økosystem", "leveområd", "miljø", "økolog", "rovdyr", "pattedyr", "dyreart", "dyrart", "planter", "artsmangf", "biologisk diversit", "biologisk mangf", "biomangf"] 
termlist15_1w = ["art", "arter"]

phrasedefault15_1s = r'(?:{})'.format('|'.join(termlist15_1s))
phrasespecific15_1tcase = r'\b(?:{})\b'.format('|'.join(termlist15_1tcase))
phrasespecific15_1u = r'\b(?:{})\b'.format('|'.join(termlist15_1u))
phrasedefault15_1v = r'(?:{})'.format('|'.join(termlist15_1v))
phrasespecific15_1w = r'\b(?:{})\b'.format('|'.join(termlist15_1w))
```


```python
#Search 1

Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_1s, na=False, case=False))
        | (Data['result_title'].str.contains(phrasespecific15_1tcase, na=False, case=True)) #case = True
        |
        (
            (Data['result_title'].str.contains(phrasespecific15_1u, na=False, case=False))
            & ((Data['result_title'].str.contains(phrasedefault15_1v, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_1w, na=False, case=False))) 
        )
    )
    &(Data['terrestrial_double_NOT']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```

### SDG 15.2

*15.2 By 2020, promote the implementation of sustainable management of all types of forests, halt deforestation, restore degraded forests and substantially increase afforestation and reforestation globally*

*Innen 2020 fremme innføringen av en bærekraftig forvaltning av all slags skog, stanse avskoging, gjenopprette forringede skoger, og i betydelig grad øke gjenreising og nyplanting av skog på globalt nivå.*

Norsk Skogseierforbund (https://skog.no) and Landbruksdirektoratet (https://www.landbruksdirektoratet.no/nb/skogbruk/skogskjotsel) websites were used to help with translation of forestry terms.

#### Phrase 1


```python
#Termlists
termlist15_2a = ["sustainable forest","sustainable woodland","sustainable silvicultur","sustainable arboricultur",
                 "protected forest", "reserved forest", 
                 "UN strategic plan for forests", "global forest goals",

                 "bærekraftfig skog", "bærekraftig silvikultur", "berekraftig skog", "berekraftig silvikult",
                 "vernet skog", "vern av skog", "bevarte skog", "bevart skog", "freda skog", "skogvern", "verneområder i skog",
                 "strategiske plan for skog"]
termlist15_2acaps = ["UNSPF", "GFG"]

termlist15_2b = ["sustainab", "responsibl", "environmental", "ecological",
                 "bærekraftig", "berekraftig", "ansvarlig", "ansvarleg","miljøbevisst", "miljøvennlig","miljøvennleg", "økologisk"]

termlist15_2c = ["manag", "govern", "development", "administ", "planning", "policy", "policies", "strateg", "approach",
                 "practice", "method", "forestry",
                 "cutting", "logging", "felling", "clearing", "lopping", "limbing", "thinning", "creaming", "pruning", "rotation",
                 "planting tree", "tree planting", "drainage", 
                 "forest area change",
                 "above ground biomass",
                 "protected area", "term management plan",
                 "forest under certification",
                 "certified forest area",

                 "forvalt", "styring", "ledelse", "leiing", "utvikling", "planlegg", "politikk", "retningslin", "tilnærming",
                 "praksis", "metode", "skogskjøtsel", "skogpleie", "skogsvirke",
                 "tynning", "gjødsling", "hogst", "hogge", "stelle",
                 "planting", "foryngelse", "gjengro", "attgro", "restaurer", "drenering",
                 "skogområde", "skogvolum", "skogdek", "skogbevokste områd", "skogbevokst områd","skogareal",
                 "miljøvern", "bevaret", "bevaring", "fredet", "fredning", "frivillig vern",
                 "miljøsertifi"]
termlist15_2ctrunc = ["use", "usage", "using", "cut",
                      "bruk", "skogbruk.*"]

termlist15_2d = ["forest", "woodland", "silvicultur", "arboricultu",
                 "skog", "silvikultur"]

phrasedefault15_2a = r'(?:{})'.format('|'.join(termlist15_2a))
phrasedefault15_2acaps = r'(?:{})'.format('|'.join(termlist15_2acaps))
phrasedefault15_2b = r'(?:{})'.format('|'.join(termlist15_2b))
phrasedefault15_2c = r'(?:{})'.format('|'.join(termlist15_2c))
phrasedefault15_2ctrunc = r'(?:{})'.format('|'.join(termlist15_2ctrunc))
phrasedefault15_2d = r'(?:{})'.format('|'.join(termlist15_2d))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_2a, na=False, case=False)) 
    | (Data['result_title'].str.contains(phrasedefault15_2acaps, na=False, case=True)) #case = True
    | 
    (
        (Data['result_title'].str.contains(phrasedefault15_2b, na=False, case=False))
        & ((Data['result_title'].str.contains(phrasedefault15_2c, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault15_2ctrunc, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault15_2d, na=False, case=False))
    )
),"tempsdg15_02"] = "SDG15_02"

print("Number of results = ", len(Data[(Data.tempsdg15_02 == "SDG15_02")]))  
```


```python
test=Data.loc[(Data.tempsdg15_02 == "SDG15_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist15_2e = ["deforest", "de-forest",
                 "avskog", "skogforringelse", "skogtap"]
#skogforringelse (NO: forest degredation), and is included here instead of below because in Norwegian this is specific to forests.

termlist15_2f = ["forests", "woodland", "silvicultur", "arboricultu",
                 "skoger", "silvikultur"]
termlist15_2f_trunc = ["forest",
                       "skog"] 
#Here we don't allow right truncation because "forest" can find "forestillinger"(NO), and "skog"(NO) finds "skogsfugl" etc. 
#Left truncation still allows "rainforest" etc.            

termlist15_2g = ["losses", "degradation", "decreas", "reduc", "mitigat", "disappear",
                 "fortapt", "forring", "reduksj", "nedgang", "mindre", "forsvinn", "forsvunn", "naturtap"]
termlist15_2gtrunc = ["loss", "lost", 
                      "tap", "tapt"]

termlist15_2hcase = ["REDD"] 

phrasedefault15_2e = r'(?:{})'.format('|'.join(termlist15_2e))
phrasedefault15_2f = r'(?:{})'.format('|'.join(termlist15_2f))
phrasespecific15_2ftrunc = r'(?:{})\b'.format('|'.join(termlist15_2f_trunc))
phrasedefault15_2g = r'(?:{})'.format('|'.join(termlist15_2g))
phrasespecific15_2gtrunc = r'\b(?:{})\b'.format('|'.join(termlist15_2gtrunc))
phrasedefault15_2hcase = r'(?:{})'.format('|'.join(termlist15_2hcase))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_2e, na=False, case=False)) 
    | (Data['result_title'].str.contains(phrasedefault15_2hcase, na=False, case=True)) #case=T
    | 
    (
        ((Data['result_title'].str.contains(phrasedefault15_2f, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_2ftrunc, na=False, case=False)))
        & ((Data['result_title'].str.contains(phrasedefault15_2g, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_2gtrunc, na=False, case=False)))
    )
),"tempsdg15_02"] = "SDG15_02"

print("Number of results = ", len(Data[(Data.tempsdg15_02 == "SDG15_02")]))  
```


```python
test=Data.loc[(Data.tempsdg15_02 == "SDG15_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
#Here we have changed the structure to accomodate that we can't use NEAR, so some terms are combined in phrases.

termlist15_2i = ["afforest", "reforest", "re-forest",
                 "increase forest cover", "increasing forest cover","increase forest area", "increasing forest area",
                 "skogplanting", "planting av skog", 
                 ]

termlist15_2l = ["skogområde", "skogvolum", "skogdek", "skogbevokste områd", "skogbevokst områd","skogareal"]
termlist15_2m = [" øk", " auk", "høyere", "høgre", "høgare", "større", "utvid"] #space before "øk"(NO) and "auk"(NO) added to prevent left truncation

termlist15_2j = ["forests", "woodland",
                 "skoger", "skogar"]
termlist15_2j_trunc = ["forest",
                       "skog"] 
    #Here we don't allow right truncation because "forest" can find "forestillinger"(NO), and "skog"(NO) finds "skogsfugl" etc. 
    #Left truncation still allows "rainforest" etc.

termlist15_2k = ["restor", "rehabilit", "increase cover",
                 "restaur", "gjengro", "attgro", "gjenopprett", "gjenreis", "nyplanting"]

phrasedefault15_2i = r'(?:{})'.format('|'.join(termlist15_2i))
phrasedefault15_2j = r'(?:{})'.format('|'.join(termlist15_2j))
phrasespecific15_2jtrunc = r'(?:{})\b'.format('|'.join(termlist15_2j_trunc))
phrasedefault15_2k = r'(?:{})'.format('|'.join(termlist15_2k))
phrasedefault15_2l = r'(?:{})'.format('|'.join(termlist15_2l))
phrasedefault15_2m = r'(?:{})'.format('|'.join(termlist15_2m))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_2i, na=False, case=False)) 
    | ((Data['result_title'].str.contains(phrasedefault15_2l, na=False, case=False))& (Data['result_title'].str.contains(phrasedefault15_2m, na=False, case=False)))
    |
    (
        ((Data['result_title'].str.contains(phrasedefault15_2j, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_2jtrunc, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault15_2k, na=False, case=False))
    )
),"tempsdg15_02"] = "SDG15_02"

print("Number of results = ", len(Data[(Data.tempsdg15_02 == "SDG15_02")]))  
```


```python
test=Data.loc[(Data.tempsdg15_02 == "SDG15_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.3

*15.3 By 2030, combat desertification, restore degraded land and soil, including land affected by desertification, drought and floods, and strive to achieve a land degradation-neutral world*

*Innen 2030 bekjempe ørkenspredning, restaurere forringet land og matjord, inkludert landområder som er rammet av ørkenspredning,   tørke og flom, og arbeide for en verden uten landforringelse.*

The Store Norske Leksikon was used to help translate terms (https://snl.no/%C3%B8rkenspredning).

#### Phrase 1


```python
#Termlists
termlist15_3a = ["desertific", "convention to combat desertification",
                "ørkenspredning", "ørkenspreiing", "forørkning", "konvensjon for bekjempelse av ørkenspredning", "forørkningskonvensjon"
                ]
termlist15_3acaps = ["UNCCD"]

termlist15_3b = ["increas", "expand", "expansion",
                 "økning", "utvid", "spredning", "spreiing", " auk" #space before " auk" to prevent left truncation
                ]
termlist15_3c = ["desert", "drylands", "dryland area",
                 "ørken", "halvtørr"]

phrasedefault15_3a = r'(?:{})'.format('|'.join(termlist15_3a))
phrasedefault15_3acaps = r'(?:{})'.format('|'.join(termlist15_3acaps))
phrasedefault15_3b = r'(?:{})'.format('|'.join(termlist15_3b))
phrasedefault15_3c = r'(?:{})'.format('|'.join(termlist15_3c))
```


```python
#Search 1

Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_3a, na=False, case=False)) 
    |(Data['result_title'].str.contains(phrasedefault15_3acaps, na=False, case=True)) #case=T
    | 
    (
        (Data['result_title'].str.contains(phrasedefault15_3b, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault15_3c, na=False, case=False))
    )
),"tempsdg15_03"] = "SDG15_03"

print("Number of results = ", len(Data[(Data.tempsdg15_03 == "SDG15_03")]))  
```


```python
test=Data.loc[(Data.tempsdg15_03 == "SDG15_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist15_3d = ["desertific", "drought", "flood", "drylands", "dryland area", 
                 "ørkenspredning", "ørkenspreiing", "halvtørre område", "tørrland"]

termlist15_3e = ["soil structure" , "soil fertility", "soil health",
                 "soil quality", "land quality",
                 "jordskjelett", "jordstruktur", "fruktbar jord", "jordhelse",
                 "jordkvalitet", "kvalitetsjord"]

termlist15_3f = ["land", "soil",
                 "jord", "dyrket mark", "dyrkamark", "kultivert mark"]

termlist15_3g = ["quality", "fertility", "degrad", "erosion", "eroded",
                 "kvalitet", "fruktbar", "forring", "erosjon", "jordtap"]

phrasedefault15_3d = r'(?:{})'.format('|'.join(termlist15_3d))
phrasedefault15_3e = r'(?:{})'.format('|'.join(termlist15_3e))
phrasedefault15_3f = r'(?:{})'.format('|'.join(termlist15_3f))
phrasedefault15_3g = r'(?:{})'.format('|'.join(termlist15_3g))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_3d, na=False, case=False)) 
    & 
    (
        (Data['result_title'].str.contains(phrasedefault15_3e, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault15_3f, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault15_3g, na=False, case=False)))
    )
),"tempsdg15_03"] = "SDG15_03"

print("Number of results = ", len(Data[(Data.tempsdg15_03 == "SDG15_03")]))  
```


```python
test=Data.loc[(Data.tempsdg15_03 == "SDG15_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists

termlist15_3h = ["aridificat", "soil pollution", "soil loss"] #Translations of these (e.g."uttørking"(NO)) are combined with soil terms in 3j

termlist15_3i = ["soil",
                 "dyrket mark", "dyrkamark", "dyrka mark", "dyrkamark",  "kultivert mark"]
termlist15_3itrunc = ["land", "jord", "jordbruk"] 
#"land" is not truncated because in Norwegian it is a part of many place names, also in english (e.g. LANDSAT, Iceland...), and "jord"(NO) due to "fjord"
# land still creates some noise in Norwegian ("land"(NO) = "country"(EN)) - but not enough to make it worth losing English combinations (land quality, land erosion)?
termlist15_3j = ["quality", "degrad", "erosion", "eroded", "salinisat", "alkalinisat", "acidificat", "contaminat", "pollution", "biodiversity loss",
                 "kvalitet", "forring", "uttørking", "erosjon", "jordtap", "salinering", "forsalting", "forsuring", "forurein", "forurensing"]

termlist15_3k = ["declin","decreas","reduc","degrad","lower","loss",
                 "nedgang", "mindre", "forring", "lavere", "lægre", "lågare"]
termlist15_3k_trunc = ["tap", "tapt", "tapte"]
termlist15_3l = ["biodiversity","soil","vegetation","groundwater",
                 "biodiversitet", "biologisk diversitet", "biologisk mangf", "biomangf", "jord", "vegetasjon", "grunnvann", "grunnvatn"]

termlist15_3m = ["desert", "drylands", "dryland area", "sub-humid", "sub humid", "semi-arid", "semiarid",
                 "ørken", "halvtørr", "tørrland"]
termlist15_3mtrunc = ["arid"]

phrasedefault15_3h = r'(?:{})'.format('|'.join(termlist15_3h))
phrasedefault15_3i = r'(?:{})'.format('|'.join(termlist15_3i))
phrasespecific15_3itrunc = r'\b(?:{})\b'.format('|'.join(termlist15_3itrunc))
phrasedefault15_3j = r'(?:{})'.format('|'.join(termlist15_3j))
phrasedefault15_3k = r'(?:{})'.format('|'.join(termlist15_3k))
phrasespecific15_2ktrunc = r'\b(?:{})\b'.format('|'.join(termlist15_3k_trunc))
phrasedefault15_3l = r'(?:{})'.format('|'.join(termlist15_3l))
phrasedefault15_3m = r'(?:{})'.format('|'.join(termlist15_3m))
phrasespecific15_2mtrunc = r'\b(?:{})\b'.format('|'.join(termlist15_3mtrunc))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_3h, na=False, case=False)) 
    | (
        ((Data['result_title'].str.contains(phrasedefault15_3i, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific15_3itrunc, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault15_3j, na=False, case=False))
      )
    |
    (
        ((Data['result_title'].str.contains(phrasedefault15_3k, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_2ktrunc, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault15_3l, na=False, case=False))
        & ((Data['result_title'].str.contains(phrasedefault15_3m, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_2mtrunc, na=False, case=False)))
    )
),"tempsdg15_03"] = "SDG15_03"

print("Number of results = ", len(Data[(Data.tempsdg15_03 == "SDG15_03")]))  
```


```python
test=Data.loc[(Data.tempsdg15_03 == "SDG15_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4

Note, "land degredation" is already covered by phrase 3, and "LDN" only brings noise here, so it is not included (low-dose naltrexone).


```python
#Termlists
termlist15_3n = ["protect", "conserv", "preserv", "restor", "rehabilit", 
                 "promot", "improv", "enhanc", "strengthen", "maintain",
                 
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaure",
                 "forbedr", "sterke", "vedlikehold", "forvalt",]

termlist15_3o = ["soil",
                 "dyrkbar jord", "dyrka jord", "dyrkajord", "dyrket jord", "matjord", "jordmass", "jordvern", "dyrket mark", "dyrkamark", "dyrka mark", "kultivert mark"]
#"jord"(NO) is added in phrases here as the terms it is combined with (AND) are a lot more general than in the other phrases - causes issues with e.g. "Jordan"(EN/NO) or "fjord"(EN/NO) or "gjorde"(NO).

termlist15_3p = ["fertility", "productivity", "stucture", "health", "protect", "conserv", "preserv", "restor", "rehabilit",
                 "fruktbar", "fertilitet", "produktivitet", "helse", "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaure"]
                
phrasedefault15_3n = r'(?:{})'.format('|'.join(termlist15_3n))
phrasedefault15_3o = r'(?:{})'.format('|'.join(termlist15_3o))
phrasedefault15_3p = r'(?:{})'.format('|'.join(termlist15_3p))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_3n, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault15_3o, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault15_3p, na=False, case=False))
),"tempsdg15_03"] = "SDG15_03"

print("Number of results = ", len(Data[(Data.tempsdg15_03 == "SDG15_03")])) 
```


```python
test=Data.loc[(Data.tempsdg15_03 == "SDG15_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.4

*15.4 By 2030, ensure the conservation of mountain ecosystems, including their biodiversity, in order to enhance their capacity to provide benefits that are essential for sustainable development*

*Innen 2030 bevare økosystemer i fjellområder, inkludert det biologiske mangfoldet der, slik at de skal bli bedre i stand til å bidra til en bærekraftig utvikling*

#### Phrase 1 & 2 
Since phrase 1 and 2 use many of the same terms, they are both handled here. For the original phrase 2, I have simplified by only taking the terms "sustainable", "ecologial" and "environmental" and dropped the combination with use, management etc. as this is a title search. In an abstract search they should probably be included. I have also allowed some area-conservation terms (e.g. "nature reserve") to be combined with mountain/alpine alone, instead of area-conservation + mountain/alpine + nature/ecosystem. 


```python
#Termlists
termlist15_4a = ["mountain", "alpine", "highland", "montane",         
                 "fjell", "alpin", "vidde", "vidda"]

termlist15_4b = ["manag", "conserv", "protect", "restor", "rehabilit",
                 "increas","strengthen","improv","enhanc","better","higher","upgrad","advance","develop","ensure","maintain","preserv","sustain",
                 "decreas","reduc","restrict","degrad","lower","declin","deterior",
                 "coping","cope","adapt","resilien",
                 "assess","examin","evaluat","measur","monitor",
                 "govern", "administra", "planning", "policy", "policies", "strateg", "approach",
                 "sustainable", 

                 "styring", "forvalt", "vernet", "verna", "verne", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaur",
                 "øker", "styrk", "forbedr", "bedring", "betring", "oppgrad", "viderefør", "sikre", "vedlikehold", "vedlikehald", "oppretthold", "opprethald",
                 "reduser", "nedgang", "avgrens", "forring", "nedsatt", "nedsett", 
                 "tåle", "tilpass", "resilien",
                 "overvåk", "vurder", "evaluer", "måle", "monitor",
                 "styring", "ledels", "leiing", "planlegg", "politikk",
                 "bærekraft", "berekraft", ]

termlist15_4c = ["ecosystem", "habitat",
                 "diversity",
                 "key species","keystone species","foundation species","habitat forming species","habitat-forming species","key resource",
                 "cover",
                 "ecological", "environmental",

                 "økosystem", "miljø", "leveområd", 
                 "mangfold", "mangfald", "diversitet", 
                 "nøkkelart", "flaggskipsart", "paraplyart", "nøkkelressurs",
                 "dekning", "dekke",
                 "økologi", "miljø"]

termlist15_4d = ["Protected area","Wilderness area", "nature conservation",
                 "Nature reserve","National park","Natural monument","Natural feature","Protected landscape",
                 "Habitat management area", "Species management area",
                 "key biodiversity area", "important sites for biodiversity",
                 "Mountain Partnership", "Mountain Green Cover Index",
                 "Convention on Biological Diversity", 
                 "Convention on International Trade in Endangered Species of Wild Fauna and Flora",
                 
                 "vernområde", "verneområde", "naturvern",
                 "naturreservat", "biotopvernområde", "nasjonalpark", "bevarte område", "bevaringsområde",
                 "områdevern", "økosystembasert forvalt", "økosystembasert styring", "forvaltningsplan", "bærekraftig forvalt", "berekraftig forvalt","arealforvaltning", 
                 "artsforvaltning", "naturmangfoldloven", "lov om vern av naturens mangfold",
                 "Konvensjonen om biologisk mangfold", "Konvensjon om biologisk mangfold", "biodiversitetskonvensjon", 
                 "Konvensjonen om internasjonal handel med truede dyr", "naturmangfoldloven"]

termlist15_4d_case = ["KBA", "KBAs", "CBD", "CITES"]

phrasedefault15_4a = r'(?:{})'.format('|'.join(termlist15_4a))
phrasespecific15_4b = r'(?:{})'.format('|'.join(termlist15_4b))
phrasedefault15_4c = r'(?:{})'.format('|'.join(termlist15_4c))
phrasedefault15_4d = r'(?:{})'.format('|'.join(termlist15_4d))
phrasespecific15_4d_case = r'\b(?:{})\b'.format('|'.join(termlist15_4d_case))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_4a, na=False, case=False)) 
    & 
    (
        (Data['result_title'].str.contains(phrasedefault15_4d, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasespecific15_4d_case, na=False, case=True)) #case=T
        | ((Data['result_title'].str.contains(phrasespecific15_4b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault15_4c, na=False, case=False)))
    )
),"tempsdg15_04"] = "SDG15_04"

print("Number of results = ", len(Data[(Data.tempsdg15_04 == "SDG15_04")]))  
```


```python
test=Data.loc[(Data.tempsdg15_04 == "SDG15_04"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.5
*15.5 Take urgent and significant action to reduce the degradation of natural habitats, halt the loss of biodiversity and, by 2020, protect and prevent the extinction of threatened species*

*Iverksette umiddelbare og omfattende tiltak for å redusere ødeleggelsen av habitater, stanse tap av biologisk mangfold og innen 2020 verne truede arter og forhindre at de dør ut*

The Norwegian Red List (Artsdatabanken) webpages were used for Norwegian terms (https://artsdatabanken.no/lister/rodlisteforarter/2021/)

#### Phrase 1


```python
#Termlists
termlist15_5a = ["degrad", "declin", "loss", "lost", "destruct", "disappear", "fragment",
                 "forring", "nedgang", "taper", "tapt", "miste", "ødelegg", "ødelag", "øydelegg", "øydelag", "forsvinn"]
termlist15_5a_trunc = ["tap","tape"] 

termlist15_5b = ["ecosystem","biotope","habitat",
                 "økosystem", "biotop", "leveområd"] 

termlist15_5c = ["communit",
                 "samfunn"] 

termlist15_5d = ["ecolog", "species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird", "moss", "tree", "grassland", "pollinat",
                 "økologi", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl", "moser", "mosar", "trær"]
termlist15_5d_trunc = ["art","arter","dyr"] 

phrasedefault15_5a = r'(?:{})'.format('|'.join(termlist15_5a))
phrasedefault15_5a_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_5a_trunc))
phrasedefault15_5b = r'(?:{})'.format('|'.join(termlist15_5b))
phrasedefault15_5c = r'(?:{})'.format('|'.join(termlist15_5c))
phrasedefault15_5d = r'(?:{})'.format('|'.join(termlist15_5d))
phrasedefault15_5d_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_5d_trunc))
```


```python
#Search 1 - in terrestrial terms
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault15_5a, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault15_5a_trunc, na=False, case=False)))
        &    
        ((Data['result_title'].str.contains(phrasedefault15_5b, na=False, case=False))
        |
         (
            (Data['result_title'].str.contains(phrasedefault15_5c, na=False, case=False)) 
            & ((Data['result_title'].str.contains(phrasedefault15_5d, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault15_5d_trunc, na=False, case=False)))
         )
        )
    )
    &(Data['terr_terms']==True)
),"tempsdg15_05"] = "SDG15_05"

print("Number of results = ", len(Data[(Data.tempsdg15_05 == "SDG15_05")]))  
```


```python
test=Data.loc[(Data.tempsdg15_05 == "SDG15_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
#Use same terms as 15_5a

termlist15_5e = ["diversity", "species",
                 "diversitet", "mangfold", "mangfald"] 
termlist15_5e_trunc = ["art","arter"] 

phrasedefault15_5e = r'(?:{})'.format('|'.join(termlist15_5e))
phrasedefault15_5e_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_5e_trunc))
```


```python
#Search 1 - in terr
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault15_5a, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault15_5a_trunc, na=False, case=False)))
        &    
        ((Data['result_title'].str.contains(phrasedefault15_5e, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault15_5e_trunc, na=False, case=False)))
    )
    & (Data['terr_terms']==True)
)]

print("Number of results = ", len(Data[(Data.tempsdg15_05 == "SDG15_05")]))  
```


```python
test=Data.loc[(Data.tempsdg15_05 == "SDG15_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists

termlist15_5f = ["manag", "conserv", "protect", "restor", "rehabilit", "preserv",
                 "increas","strengthen","improv","enhanc","better","higher","upgrad","advance","develop","ensure","maintain","preserv","sustain",
                 "decreas","reduc","restrict","degrad","lower","declin","deterior"," loss"
                 "coping","cope","adapt","resilien",
                 "assess","examin","evaluat","measur","monitor",

                 "styring", "forvalt", "verne", "verna", "vern av", "miljøvern", "bevare", "betring", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaur",
                 "øker", "styrk", "forbedr", "bedring", "oppgrad", "viderefør", "sikre", "vedlikehold", "vedlikehald", "oppretthold", "opprethald",
                 "reduser", "nedgang", "avgrens", "forring", "nedsatt", "nedsett", "tap av",
                 "tåle", "tilpas", "resilien",
                 "overvåk", "overvak", "vurder", "evaluer", "måle", "monitor"]

termlist15_5g = ["biodiversity","species diversity",
                "red list", "International Union for Conservation of Nature",

                "artsmangf", "artsdiversitet", "biomangf", "biologisk mangf", "biologiske mangf", "naturmangf",
                "artsforvaltning", "naturmangfoldloven", "lov om vern av naturens mangfold",
                "rødlist", "rød list", "raudlist", "raud list",
                "trua art", "trued art", "truede art"] 
                 #"trua art" (NO) etc are included as phrases here because both terms are easily creating noise with automatic truncation
                 #The english combinations and "truet"(NO) are covered by h+i below
termlist15_5g_case = ["KBA", "KBAs", "CBD", "RLI", "IUCN"]

termlist15_5h = ["threatened","near extinct","at risk","endanger","vulnerable","protected","red list",
                 "diversity",
                 "truet", "truga", "utryddingstru", "utrydjingstruga", "utsatte", "utsette", "sårbar", "vernet", "verna", "fredet", "freda", "rødlist", "rød list", "raudlist", "raud list",
                 "diversitet", "mangfold", "mangfald"]

termlist15_5i = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl", "moser", "mosar", "trær"]
termlist15_5i_trunc = ["art","arter","dyr"]  

phrasedefault15_5f = r'(?:{})'.format('|'.join(termlist15_5f))
phrasedefault15_5g = r'(?:{})'.format('|'.join(termlist15_5g))
phrasedefault15_5g_case = r'\b(?:{})\b'.format('|'.join(termlist15_5g_case))
phrasedefault15_5h = r'(?:{})'.format('|'.join(termlist15_5h))
phrasedefault15_5i = r'(?:{})'.format('|'.join(termlist15_5i))
phrasedefault15_5i_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_5i_trunc))
```


```python
#Search 1 - in terr double NOT
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_5f, na=False, case=False)) 
        & 
        (
            ((Data['result_title'].str.contains(phrasedefault15_5g, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_5g_case, na=False, case=True)))
            | 
            ((Data['result_title'].str.contains(phrasedefault15_5h, na=False, case=False))
            & ((Data['result_title'].str.contains(phrasedefault15_5i, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_5i_trunc, na=False, case=False)))
            )
        )
    )
    &(Data['terrestrial_double_NOT']==True)
)]

print("Number of results = ", len(Data[(Data.tempsdg15_05 == "SDG15_05")]))  
```


```python
test=Data.loc[(Data.tempsdg15_05 == "SDG15_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4


```python
#Termlists
termlist15_5j = ["threatened","near extinct","at risk","endanger","vulnerable","protected","red list",
                 "truet", "truga", "trua ", " trued", "truede", "utryddingstru", "utrydjingstruga", "utsatte", "utsette", "sårbar", "vernet", "verna", "fredet", "freda", "rødlist", "rød list", "raudlist", "raud list"] 
#the spaces before/after "trua"(NO), "trued"(NO) are intentional (to avoid e.g. "construed")

termlist15_5k = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]
termlist15_5k_trunc = ["art", "arter", "dyr"]  

termlist15_5l = ["extinction", "loss", "going extinct",
                 "utrydd", "utrydj", "tapt", "miste", "mista"]
termlist15_5l_trunc = ["tap", "tape"]                 

phrasedefault15_5j = r'(?:{})'.format('|'.join(termlist15_5j))
phrasedefault15_5k = r'(?:{})'.format('|'.join(termlist15_5k))
phrasedefault15_5k_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_5k_trunc))
phrasedefault15_5l = r'(?:{})'.format('|'.join(termlist15_5l))
phrasedefault15_5l_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_5l_trunc))
```


```python
#Search 1
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault15_5l, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault15_5l_trunc, na=False, case=False)))
        &    
        (
            (Data['result_title'].str.contains(phrasedefault15_5j, na=False, case=False))
            & ((Data['result_title'].str.contains(phrasedefault15_5k, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_5k_trunc, na=False, case=False)))
        )
    )
    &(Data['terrestrial_double_NOT']==True)
)]

print("Number of results = ", len(Data[(Data.tempsdg15_05 == "SDG15_05")]))  
```


```python
test=Data.loc[(Data.tempsdg15_05 == "SDG15_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.6

*15.6 Promote fair and equitable sharing of the benefits arising from the utilization of genetic resources and promote appropriate access to such resources, as internationally agreed*

*Fremme en rettferdig og likeverdig deling av godene knyttet til bruk av genressurser, og fremme formålstjenlig tilgang til slike ressurser i  tråd med internasjonal enighet*

#### Phrase 1


```python
#Termlists
termlist15_6a = ["share", "sharing", "equitab", "equal", "fair", "access", "right", "ownership", "appropriati", "biopira", "biocoloni", "using", "utiliz", "utilis", "use of",
                 "deling", "deler", " dele"  "tilgang", "rett", "rettferd", "eierskap", "eigarskap", "bruk av", "bruker", "utnytte"] 
#spaces around "dele"(NO) intentional to avoid truncation

termlist15_6b = ["genetic resource", "gene resource", "bioresource", "biological resource",
                 "traditional knowledge", "indigenous knowledge", "autochthonous knowledge", "local knowledge",

                 "genetiske ressurs", "genressurs", "plantegenetiske ressurs", "dyrgenetiske ressurs", "dyregenetiske ressurs", "bioressurs", "biologiske ressurs",
                 "tradisjonelle kunnskap", "tradisjonell kunnskap", "urfolkskunnskap"]

termlist15_6c = ["ecosystem", "biotop", "diversity", "species", "plant", "animal", "organism", 
                 "økosystem", "diversit", "mangfold", "mangfald", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "dyrgenetiske", "dyrgenetiske"] 
termlist15_6c_trunc = ["art", "arter", "dyr"]  

phrasedefault15_6a = r'(?:{})'.format('|'.join(termlist15_6a))
phrasedefault15_6b = r'(?:{})'.format('|'.join(termlist15_6b))
phrasedefault15_6c = r'(?:{})'.format('|'.join(termlist15_6c))
phrasedefault15_6c_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_6c_trunc))
```

In the WOS string,  6a and 6b are run with 6c against the double NOT terrestrial set. Here we carry out an additional search, since these are quite specific terms, where 6a and 6b are also run with AND against the terrestrial set (e.g. publications with genetic resource sharing + forests can be found)


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_6a, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault15_6b, na=False, case=False))
        & ((Data['result_title'].str.contains(phrasedefault15_6c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_6c_trunc, na=False, case=False)))
        & (Data['terrestrial_double_NOT']==True)
    )
    |
    (
        (Data['result_title'].str.contains(phrasedefault15_6a, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault15_6b, na=False, case=False))
        & (Data['terr_terms']==True)
    )
),"tempsdg15_06"] = "SDG15_06"

print("Number of results = ", len(Data[(Data.tempsdg15_06 == "SDG15_06")])) 
```


```python
test=Data.loc[(Data.tempsdg15_06 == "SDG15_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2 & 3 


```python
#Termlists
#Re-use 6b and 6c

termlist15_6d = ["benefit", "results", "transfer", "technolog", "participat", "product", "monetary", "royalties", "compensat", "bioprospect",
                 "fordel", "gevinst", "resultat", "overfør", "teknologi", "deltak", "finansiel", "kompensasj", "godtgjørelse", "godtgjer", "bioprospekt"] 

termlist15_6e = ["Nagoya", "Convention on biological diversity", "benefit sharing", "benefit-sharing",
                 "Plant Genetic Resources for Food and Agriculture",
                 "Konvensjonen om biologisk mangfold", "biodiversitetskonvensjon", "Den internasjonale plantetraktaten"
                ] 
termlist15_6e_case = ["CBD","ABS","PGRFA"]

termlist15_6f = ["Access and benefit sharing", "Access and benefit-sharing",  "Bonn guideline"]

phrasedefault15_6d = r'(?:{})'.format('|'.join(termlist15_6d))
phrasedefault15_6e = r'(?:{})'.format('|'.join(termlist15_6e))
phrasedefault15_6e_case = r'(?:{})'.format('|'.join(termlist15_6e_case))
phrasedefault15_6f = r'(?:{})'.format('|'.join(termlist15_6f))
```


```python
#Search 1 - slightly simplified compared to WOS due to title search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_6b, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault15_6d, na=False, case=False))
        & ((Data['terr_terms']==True) | (Data['result_title'].str.contains(phrasedefault15_6c, na=False, case=False)))
    )
    |
    (
        (Data['result_title'].str.contains(phrasedefault15_6b, na=False, case=False)) 
        & ((Data['result_title'].str.contains(phrasedefault15_6e, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_6e_case, na=False, case=True))) #case=T
        & (Data['terr_terms']==True)
    )
    | (Data['result_title'].str.contains(phrasedefault15_6f, na=False, case=False))
),"tempsdg15_06"] = "SDG15_06"

print("Number of results = ", len(Data[(Data.tempsdg15_06 == "SDG15_06")]))  
```


```python
test=Data.loc[(Data.tempsdg15_06 == "SDG15_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.7

*15.7 Take urgent action to end poaching and trafficking of protected species of flora and fauna and address both demand and supply of illegal wildlife products*

*Iverksette umiddelbare tiltak for å stanse krypskyting og ulovlig handel med vernede plante- og dyrearter, og håndtere både tilbuds- og etterspørselssiden ved handelen med ulovlige produkter fra viltlevende dyr*

#### Phrase 1


```python
#Termlists
termlist15_7a = ["poach", "traffick", "smuggl",
                 "krypskyt", "ulovlig", "ulovleg", "smugl"]

#termlist15_7b = ["protected", "endanger", "threat", "extinct", "at risk", "vulnerable", "red list",
#                 "truet", "truga", "utryddingstru", "utrydjingstruga", "utsatte", "utsette", "sårbar", "vernet", "verna", "fredet", "freda", "rødlist", "rød list", "raudlist", "raud list"]
#Taken out of newest version

termlist15_7c = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]  

termlist15_7c_trunc = ["art", "arter", "dyr"]                                  

termlist15_7d = ["rosewood" , "kosso" , "elephant" , "rhino" , "ivory" , "pangolin" , "turtle" , "tortoise" , "big cat" , "tiger" , "glass eel",      
                 "elefant", "neshorn", "elfenbein", "elfenben", "skilpadde", "store katt", "glassål"]

phrasedefault15_7a = r'(?:{})'.format('|'.join(termlist15_7a))
#phrasedefault15_7b = r'(?:{})'.format('|'.join(termlist15_7b))
phrasedefault15_7c = r'(?:{})'.format('|'.join(termlist15_7c))
phrasedefault15_7c_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_7c_trunc))
phrasedefault15_7d = r'(?:{})'.format('|'.join(termlist15_7d))
```


```python
#Search 1 - terr double NOT
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_7a, na=False, case=False))
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_7c, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault15_7c_trunc, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault15_7d, na=False, case=False))
        )
    )
    &(Data['terrestrial_double_NOT']==True)
),"tempsdg15_07"] = "SDG15_07"

print("Number of results = ", len(Data[(Data.tempsdg15_07 == "SDG15_07")])) 
```


```python
test=Data.loc[(Data.tempsdg15_07 == "SDG15_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists

#Re-use c, c_trunc and d
termlist15_7e = ["illegal", "illicit", "criminal", "crime",
                 "ulovlig", "ulovleg", "krim"]

termlist15_7f = ["product" , "manufact" , "merchandise" , "artifact" , "fabricat" , "handicraft" , "handiwork",
                 "market" , "supply" , "supplier" , "supplied" , "demand" , "trade" , "trading" , "import", "export", "purchas" , "livelihood",
                 "ivory",
                 
                 "produkt", "varer", "produser", "gjenstand", "lager", "håndverk", "handverk",
                 "marked", "marknad", "etterspørsel", "tilbud", "tilbod", "handel", "kjøp", "salg", "eksport", "levebrød", "inntektskilde", "inntektskjelde",
                 "elfenbein", "elfenben"]

phrasedefault15_7e = r'(?:{})'.format('|'.join(termlist15_7e))
phrasedefault15_7f = r'(?:{})'.format('|'.join(termlist15_7f))
```


```python
#Search 1 - in terr double NOT
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_7e, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault15_7f, na=False, case=False))
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_7c, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault15_7c_trunc, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault15_7d, na=False, case=False))
        )
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_07"] = "SDG15_07"

print("Number of results = ", len(Data[(Data.tempsdg15_07 == "SDG15_07")])) 
```


```python
test=Data.loc[(Data.tempsdg15_07 == "SDG15_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists

termlist15_7g = ["International Trade in Endangered Species of Wild Fauna and Flora",
                 "Konvensjonen om internasjonal handel med truede dyr", "handel med truede og sårbare arter", "handel med truede arter"]

termlist15_7g_case = ["CITES"]

phrasedefault15_7g = r'(?:{})'.format('|'.join(termlist15_7g))
phrasespecific15_7g_case = r'\b(?:{})\b'.format('|'.join(termlist15_7g_case))
```


```python
#Search 1
# Simplified as a title search - enough just to mention CITES
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_7g, na=False, case=False))
        | (Data['result_title'].str.contains(phrasespecific15_7g_case, na=False, case=True)) #case=T
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_07"] = "SDG15_07"

print("Number of results = ", len(Data[(Data.tempsdg15_07 == "SDG15_07")])) 
```


```python
test=Data.loc[(Data.tempsdg15_07 == "SDG15_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.8

*15.8 By 2020, introduce measures to prevent the introduction and significantly reduce the impact of invasive alien species on land and water ecosystems and control or eradicate the priority species*

*Innen 2020 innføre tiltak for å unngå innføring og spredning av fremmede arter for å redusere fremmede arters påvirkning på land- og vannbaserte økosystemer i betydelig grad, og dessuten kontrollere eller utrydde prioriterte fremmede arter*

In some of the phrases I have added an additional term list specific for using these strings for Norwegian research. It contains Latin and Norwegian names for terrestrial and limnic species deemed "very high risk" in the Norwegian black list of introduced species (2018, newest version; https://www.artsdatabanken.no/fremmedartslista2018)

#### Phrase 1


```python
#Termlists
termlist15_8a = ["introduc", "spread", "expansion", "dispers", "range increas",
                 "introduser", "rømme", "forvill", "utvide", "spredning", "sprei", "spre seg", "sprer seg", "spredd seg", "utbre"]

termlist15_8b = ["invasive","alien","exotic","nonnative","non-native","nonindigenous","non-indigenous",
                  "fremmed"]

termlist15_8c = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird", "rodent",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl", "gnager",
                 "fremmedart"]  
                 #"fremmedart"(NO) is added as a term here, as in the trunc list below "art" is not allowed to be truncated. b&c will find "fremmede arter".
                 #This term can be an adjective, or e.g. "fremmedartslista"
termlist15_8c_trunc = ["art", "arter", "dyr"]       

termlist15_8d = ["Pelophylax ridibundus" , "Pelophylax lessonae" , "Pelophylax esculentus" , "Esox lucius" , "Neogobius melanostomus" , "Phoxinus phoxinus" , "Scardinius erythrophthalmus" , "Branta canadensis" , "Barbarea vulgaris" , "Bunias orientalis" , "Elodea canadensis" , "Elodea nuttallii" , "Lactuca serriola" , "Lupinus nootkatensis" , "Symphytum officinale" , "Reynoutria ×bohemica" , "Vincetoxicum rossicum" , "Epilobium ciliatum ciliatum" , "Epilobium ciliatum glandulosum" , "Aruncus dioicus" , "Lamiastrum galeobdolon argentatum" , "Lamiastrum galeobdolon galeobdolon" , "Lysimachia punctata" , "Pastinaca sativa hortensis" , "Amelanchier spicata" , "Berberis thunbergii" , "Cotoneaster bullatus" , "Cotoneaster dielsianus" , "Cotoneaster horizontalis" , "Lonicera caerulea" , "Lysimachia nummularia" , "Rosa rugosa" , "Arctium tomentosum" , "Lupinus polyphyllus" , "Rorippa ×armoracioides" , "Salix viminalis" , "Bromopsis inermis" , "Cerastium tomentosum" , "Cotoneaster lucidus" , "Heracleum mantegazzianum" , "Heracleum persicum" , "Laburnum anagyroides" , "Melilotus albus" , "Petasites japonicus giganteus" , "Petasites hybridus" , "Phedimus spurius" , "Primula elatior elatior" , "Reynoutria sachalinensis" , "Sambucus racemosa" , "Senecio viscosus" , "Sorbaria sorbifolia" , "Swida sericea" , "Vinca minor" , "Taxus ×media" , "Senecio inaequidens" , "Melilotus officinalis" , "Odontites vulgaris" , "Solidago canadensis" , "Festuca rubra commutata" , "Cotoneaster divaricatus" , "Berteroa incana" , "Pinus mugo uncinata" , "Cytisus scoparius" , "Impatiens glandulifera" , "Impatiens parviflora" , "Myrrhis odorata" , "Phedimus hybridus" , "Populus balsamifera" , "Reynoutria japonica" , "Sorbus mougeotii" , "Spiraea ×billardii" , "Spiraea ×rosalba" , "Spiraea ×rubella" , "Tsuga heterophylla" , "Alchemilla mollis" , "Pinus contorta" , "Picea sitchensis" , "Picea ×lutzii" , "Acer pseudoplatanus" , "Laburnum alpinum" , "Pinus mugo" , "Campylopus introflexus" , "Neovison vison" , "Lepus europaeus" , "Nyctereutes procyonoides" , "Sciurus carolinensis" , "Castor canadensis" , "Echinococcus multilocularis" , "Gyrodactylus salaris" , "Angiostrongylus vasorum" , "Anguillicoloides crassus" , "Bursaphelenchus xylophilus" , "Meloidogyne hapla" , "Meloidogyne minor" , "Aphanomyces astaci" , "Batrachochytrium dendrobatidis" , "Batrachochytrium salamandrivorans" , "Hymenoscyphus fraxineus" , "Phytophthora ramorum" , "Phytophthora austrocedri" , "Agrilus planipennis" , "Anoplophora glabripennis" , "Harmonia axyridis" , "Ips amitinus" , "Arion vulgaris" , "Dreissena bugensis" , "Dreissena polymorpha" , "Potamopyrgus antipodarum" , "Opilio canestrinii" , "Eriocheir sinensis" , "Daphnia parvula" , "Pacifastacus leniusculus" , "Aedes japonicus" , "Bombus terrestris" , 
                 "latterfrosk" , "kontinental damfrosk" , "hybridfrosk" , "gjedde" , "svartmunnet kutling" , "ørekyt" , "sørv" , "kanadagås" , "vinterkarse" , "russekål" , "vasspest" , "smal vasspest" , "taggsalat" , "sandlupin" , "valurt" , "hybridslirekne" , "russesvalerot" , "ugrasmjølke" , "alaskamjølke" , "skogskjegg" , "sølvtvetann" , "parkgulltvetann" , "fagerfredløs" , "hagepastinakk" , "blåhegg" , "høstberberis" , "bulkemispel" , "dielsmispel" , "krypmispel" , "blåleddved" , "krypfredløs" , "rynkerose" , "ullborre" , "hagelupin" , "hybridkulekarse" , "kurvpil" , "bladfaks" , "filtarve" , "blankmispel" , "kjempebjørnekjeks" , "tromsøpalme" , "gullregn" , "hvitsteinkløver" , "japanpestrot" , "legepestrot" , "gravbergknapp" , "lundnøkleblom" , "kjempeslirekne" , "rødhyll" , "klistersvineblom" , "rognspirea" , "alaskakornell" , "gravmyrt" , "hybridbarlind" , "boersvineblom" , "legesteinkløver" , "engrødtopp" , "kanadagullris" , "veirødsvingel" , "sprikemispel" , "hvitdodre" , "bergfuru" , "gyvel" , "kjempespringfrø" , "mongolspringfrø" , "spansk kjørvel" , "sibirbergknapp" , "balsampoppel" , "parkslirekne" , "alpeasal" , "klasespirea" , "purpurspirea" , "bleikspirea" , "vestamerikansk hemlokk" , "praktmarikåpe" , "vrifuru" , "sitkagran" , "lutzgran" , "platanlønn" , "alpegullregn" , "alpefuru" , "ribbesåtemose" , "mink " , "sørhare" , "mårhund" , "riebannjáŋkkár" , "furuvednematode" , "askeskuddbeger" , "greindreper" , "asiatisk askepraktbille" , "harlekinmarihøne" , "brunskogsnegl" , "sebramusling" , "vandrepollsnegl" , "gulrotvevkjerring" , "kinaullhåndskrabbe" , "signalkreps" , "mørk jordhumle"]
                 #Norway-specific adaptation: Added list of specific species that problematic in Norway - improves recall.

phrasedefault15_8a = r'(?:{})'.format('|'.join(termlist15_8a))
phrasedefault15_8b = r'(?:{})'.format('|'.join(termlist15_8b))
phrasedefault15_8c = r'(?:{})'.format('|'.join(termlist15_8c))
phrasedefault15_8c_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_8c_trunc))
phrasedefault15_8d = r'(?:{})'.format('|'.join(termlist15_8d))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_8a, na=False, case=False))
        & 
        (
            ((Data['result_title'].str.contains(phrasedefault15_8b, na=False, case=False)) 
            & ((Data['result_title'].str.contains(phrasedefault15_8c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_8c_trunc, na=False, case=False)))
            )
            |(Data['result_title'].str.contains(phrasedefault15_8d, na=False, case=False))
        )
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_08"] = "SDG15_08"

print("Number of results = ", len(Data[(Data.tempsdg15_08 == "SDG15_08")]))  
```


```python
test=Data.loc[(Data.tempsdg15_08 == "SDG15_08"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2 & 3

A NINA report was used to help with Norwegian terminology: *Blaalid, R., Often, A., Magnussen, K., Olsen, S. L. & Westergaard, K. B. 2017. Fremmede skadelige karplanter – Bekjempelsesmetodikk og spredningshindrende tiltak. – NINA Rapport 1432. 87 s.* http://hdl.handle.net/11250/2469573


```python
#Termlists

#Re-use b, c, d

termlist15_8e = ["impact" , "effect" , "affect" , "consequen",
                 "competition", "predation", "hybridisation", "hybridization", 
                 "disease", "parasitism",
                 "trampling", "rooting",
                 "loss", "degrad",
                 "ecosystem service", "biodiversity", 
                 "reduc","decreas","tackle","control","eradicat","remov",

                 "påvirk", "effekt", "impakt", "konsekvens",
                 "konkurrans", "predasjon", "hybridiser",
                 "sykdom", "sjukdom", "parasit",
                 "forring",
                 "økosystemtjeneste", "økosystemtenest", "biodiversitet", "biologisk mangf", "biologiske mangf", "artsmangf", "biomangf",
                 "reduser", "tiltak", "kontroll", "utrydd", "fjerne", "bekjemp", "spredningshindr", "spreiingshindr", "forebygg", "førebygg"]

termlist15_8e_trunc = ["tap", "tapt"]

phrasedefault15_8e = r'(?:{})'.format('|'.join(termlist15_8e))
phrasedefault15_8e_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_8e_trunc))

```


```python
#Search 1
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault15_8e, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_8e_trunc, na=False, case=False)))
        & 
        (
            ((Data['result_title'].str.contains(phrasedefault15_8b, na=False, case=False)) 
            & ((Data['result_title'].str.contains(phrasedefault15_8c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_8c_trunc, na=False, case=False)))
            )
            |(Data['result_title'].str.contains(phrasedefault15_8d, na=False, case=False))
        )
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_08"] = "SDG15_08"

print("Number of results = ", len(Data[(Data.tempsdg15_08 == "SDG15_08")]))  
```


```python
test=Data.loc[(Data.tempsdg15_08 == "SDG15_08"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.9

*15.9 By 2020, integrate ecosystem and biodiversity values into national and local planning, development processes, poverty reduction strategies and accounts*

*Innen 2020 integrere verdien av økosystemer og biologisk mangfold i nasjonale og lokale planleggingsprosesser, i strategier for fattigdomsbekjempelse og i regnskap*

This string has been simplified for a title search. "Biodiversity" and related terms are used more alone.


```python
#Termlists
termlist15_9d = ["National biodiversity strategy", "national biodiversity action plan"]
termlist15_9d_case = ["NBSAP"]

termlist15_9a = ["biodiversit", "biological diversity", "species diversity", " cbd",
                 "habitats", "habitat ", "biotop", "nature conserv",
                 
                 "biologisk diversitet", "biomangf", "artsmangf", "biologisk mangf", "biologiske mangf", "naturmangf",
                 "økosystem", "leveområd", "naturvern"]
#"habitat" variants are to avoid habitation

termlist15_9b = ["community", "environment", "ecosystem", "diversit", "habitat",
                 "samfunn", "miljø", "mangfold", "mangfald"]
                 #Ecosystem was 50-50 noise, so was moved here to be combined with species, plant etc. 
                 #This phrase is searched for together with 9c, and alone *within* the terrestrial set to find e.g. "forest community"

termlist15_9c = ["species", "plant", "taxonom", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "taksonom", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]

termlist15_9e = ["national", "local", "government", "regional", "sector", "municipal", "federal", "urban", "settlement", "multilevel", "multi-level",
                 "poverty reduction", "reduce poverty", "anti-poverty", "anti poverty",

                 "nasjonal", "regjering", "kommun", "lokal", "fylke", "sektor", "byer", "byområd", "byråd",
                 "fattigdom"]

termlist15_9f = ["target", "goal", "program", "strateg", "policy", "policies", "framework", "governance", 
                 "action plan", "development", "accounting", "report",

                 "handlingsplan", "planlegg", "politikk", "retningslin", "rammeverk", "styring", "ledelse", "leiing", "forvaltning", 
                 "utvikling", "rapport"]

termlist15_9f_trunc = ["plan", "planning", "plans",
                       "mål"] 

phrasedefault15_9a = r'(?:{})'.format('|'.join(termlist15_9a))
phrasedefault15_9b = r'(?:{})'.format('|'.join(termlist15_9b))
phrasedefault15_9c = r'(?:{})'.format('|'.join(termlist15_9c))
phrasedefault15_9d = r'(?:{})'.format('|'.join(termlist15_9d))
phrasedefault15_9d_case = r'(?:{})'.format('|'.join(termlist15_9d_case))
phrasedefault15_9e = r'(?:{})'.format('|'.join(termlist15_9e))
phrasedefault15_9f = r'(?:{})'.format('|'.join(termlist15_9f))
phrasespecific15_9f_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_9f_trunc))
```


```python
#Search in terr double NOT
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_9d, na=False, case=False)) 
    |(Data['result_title'].str.contains(phrasedefault15_9d_case, na=False, case=True)) #case=T
    |
    (
        ((Data['result_title'].str.contains(phrasedefault15_9a, na=False, case=False))
        |((Data['result_title'].str.contains(phrasedefault15_9b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault15_9c, na=False, case=False)))
        )
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_9e, na=False, case=False))
            & ((Data['result_title'].str.contains(phrasedefault15_9f, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_9f_trunc, na=False, case=False)))
        )
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_09"] = "SDG15_09"

print("Number of results = ", len(Data[(Data.tempsdg15_09 == "SDG15_09")]))  

#search in terr terms
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_9b, na=False, case=False))
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_9e, na=False, case=False))
            & ((Data['result_title'].str.contains(phrasedefault15_9f, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_9f_trunc, na=False, case=False)))
        )
    )
    & (Data['terr_terms']==True)
),"tempsdg15_09"] = "SDG15_09"

print("Number of results = ", len(Data[(Data.tempsdg15_09 == "SDG15_09")]))  
```


```python
test=Data.loc[(Data.tempsdg15_09 == "SDG15_09"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.a

*15.a Mobilize and significantly increase financial resources from all sources to conserve and sustainably use biodiversity and ecosystems*

*Mobilisere en betydelig økning i finansielle ressurser fra alle kilder for å bevare og utnytte biologisk mangfold og økosystemer på en bærekraftig måte*



```python
#Termlists

termlist15_aa = ["protect", "preserv", "conserv", "promot", "improv", "restor", "rehabilit",
                 "enhanc", "strengthen", "maintain", "preserv", "support",
                 
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer", 
                 "forbedr", "betre", "betring", "styrke", "vedlikeh", "støtte", "stønad"]

termlist15_ab = ["manag","use","using","govern","development","administrat","planning",
                 "forvalt", "bruk", "styr", "ledelse", "leiing", "utvikl", "planlegg"]
termlist15_ab_trunc = ["use","using",
                       "bruk"]
termlist15_ac = ["sustainabl", "responsib", "environmental", "ecological", "ecosystem",
                 "bærekraft", "berekraft", "ansvarl", "miljø", "økologisk", "økosystem"]

termlist15_ad = ["biodiversit", "biological diversity", "species diversity",
                 "habitat","biotop","nature conservation",
                 "ecosystem service", "ecosystem restor", "rio marker",
                 
                 "biologisk diversitet", "biomangf", "artsmangf", "biologisk mangf", "biologiske mangf",
                 "økosystem", "leveområd", "naturvern"]

termlist15_ae = ["community", "environment", "ecosystem", "diversit",
                 "samfunn", "miljø", "mangfold"]
                 #Ecosystem was 50-50 noise, so was moved here to be combined with species, plant etc. 
                 #This phrase is searched for together with 9af, and alone *within* the terrestrial set

termlist15_af = ["ecolog", "species", "taxonom", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "økologi", "taksonom", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]

termlist15_ag = ["investing", "investment", "investor", "financ", "spending", "funding", "grant", "funds",
                  "incentive", "taxes", "fees", "subsidy", "subsidi",
                  "cooperation fund", "development fund", "development assistance", "international aid", "international assistance", "foreign aid", "foreign assistance", 
                  "global environmental facility", "Biodiversity finance intitiative", 
                  "partnership for action on green economy", 
                  "poverty-environment action for sustainable", "poverty environment action for sustainable",
                  "green commodities program",
                 
                 "finansiel", "midlar", "økonomiske ressurs",
                 "insentiv", "skatt", "subsidier", "subsidiar", "tilskudd", "tilskot",
                 "samarbeidsfond", "utviklingsstøtte", "utviklingsstønad", "bistand", "utviklingshjelp", "u-hjelp"]
                 #"midler"(NO) is not used alone as is also in e.g. "sprøytemidler"
termlist15_9ag_case = ["GEF", "BIOFIN", "PAGE", "PEAS", "ODA"]

phrasedefault15_aa = r'(?:{})'.format('|'.join(termlist15_aa))
phrasedefault15_ab = r'(?:{})'.format('|'.join(termlist15_ab))
phrasespecific15_ab_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_ab_trunc))
phrasedefault15_ac = r'(?:{})'.format('|'.join(termlist15_ac))
phrasedefault15_ad = r'(?:{})'.format('|'.join(termlist15_ad))
phrasedefault15_ae = r'(?:{})'.format('|'.join(termlist15_ae))
phrasedefault15_af = r'(?:{})'.format('|'.join(termlist15_af))
phrasedefault15_ag = r'(?:{})'.format('|'.join(termlist15_ag))
phrasespecific15_ag_case = r'\b(?:{})\b'.format('|'.join(termlist15_9ag_case))
```

Since this is only a title search, we simplify to search for only biodiversity + investment, and drop the "sustainable use/protect" parts (when used = no results). They are commented-out below.


```python
#Search 1
Data.loc[(
    (
        #(
        #    (terrestrial_double_NOT['result_title'].str.contains(phrasedefault15_aa, na=False, case=False)) 
        #    |(
        #       (terrestrial_double_NOT['result_title'].str.contains(phrasedefault15_ac, na=False, case=False))  
        #       & ((terrestrial_double_NOT['result_title'].str.contains(phrasedefault15_ab, na=False, case=False))|(terrestrial_double_NOT['result_title'].str.contains(phrasespecific15_ab_trunc, na=False, case=False)))
        #    )
        #)
        #&
        (
            (Data['result_title'].str.contains(phrasedefault15_ad, na=False, case=False)) 
            |((Data['result_title'].str.contains(phrasedefault15_ae, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault15_af, na=False, case=False)))
            |((Data['result_title'].str.contains(phrasedefault15_ae, na=False, case=False))&(Data['terr_terms']==True)) #This line combined with terrestrial terms
        )
        &
        (
            (Data['result_title'].str.contains(phrasedefault15_ag, na=False, case=False))
            |(Data['result_title'].str.contains(phrasespecific15_ag_case, na=False, case=True))
        )
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_a"] = "SDG15_0a"

print("Number of results = ", len(Data[(Data.tempsdg15_a == "SDG15_0a")]))  
```


```python
test=Data.loc[(Data.tempsdg15_a == "SDG15_0a"), ("result_id", "result_title")]
test.iloc[0:10, ]
```

### SDG 15.b

*15.b Mobilize significant resources from all sources and at all levels to finance sustainable forest management and provide adequate incentives to developing countries to advance such management, including for conservation and reforestation*

*Mobilisere betydelige ressurser fra alle kilder og på alle nivåer for å finansiere en bærekraftig skogforvaltning, og sørge for virkemidler som er egnet til å fremme slik forvaltning i utviklingslandene, blant annet virkemidler for bevaring og nyplanting av skog*


In this search I have added a NOT search for kelp forest, as there is relatively much about this in Norway and only very rarely is a paper about both terrestrial and kelp forests. I have also simplified this search since it is a title search, by only using forests + support (not requiring + sustinable management/conservation/afforestation).


```python
#Termlists
termlist15_ba = ["investing", "investment", "investor", "financ", "spending", "funding", "grant", "funds",
                  "incentive", "taxes", "fees", "subsidy", "subsidi", "payment",
                  "cooperation fund", "development fund", "development assistance", "international aid", "international assistance", "foreign aid", "foreign assistance", 
                 
                 "finansiel", "midlar", "økonomiske ressurs", "økonomiske midler",
                 "insentiv", "skatt", "subsidier", "subsidiar", "tilskudd", "tilskot", "utbetal",
                 "samarbeidsfond", "utviklingsstøtte", "utviklingsstønad", "bistand", "utviklingshjelp", "u-hjelp"]
                 #"midler"(NO) is not used alone as is also in e.g. "sprøytemidler"
termlist15_ba_case = ["ODA"]

termlist15_bb = ["forest", "woodland", "silvicultur", "arboricultu",
                 "skog", "silvikultur"]

termlist15_bNOT = ["kelp forest"]

phrasedefault15_ba = r'(?:{})'.format('|'.join(termlist15_ba))
phrasespecific15_ba_case = r'\b(?:{})\b'.format('|'.join(termlist15_ba_case))
phrasedefault15_bb = r'(?:{})'.format('|'.join(termlist15_bb))
phrasedefault15_bNOT = r'(?:{})'.format('|'.join(termlist15_bNOT))
```


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault15_ba, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific15_ba_case, na=False, case=True))) #case = T
    & (Data['result_title'].str.contains(phrasedefault15_bb, na=False, case=False)) 
    & (~Data['result_title'].str.contains(phrasedefault15_bNOT, na=False, case=False))
),"tempsdg15_b"] = "SDG15_b"

print("Number of results = ", len(Data[(Data.tempsdg15_b == "SDG15_b")]))  
```


```python
test=Data.loc[(Data.tempsdg15_b == "SDG15_b"), ("result_id", "result_title")]
test.iloc[0:10, ]
```

### SDG 15.c
*15.c Enhance global support for efforts to combat poaching and trafficking of protected species, including by increasing the capacity of local communities to pursue sustainable livelihood opportunities*

*Øke den globale støtten til tiltak for å bekjempe krypskyting og ulovlig handel med vernede arter, blant annet ved å styrke lokalsamfunnenes evne til å benytte de muligheter som finnes for å opprettholde et bærekraftig livsgrunnlag*

#### Phrase 1


```python
#Termlists
termlist15_ca = ["poach", "traffick", "smuggl", "illegal",
                 "krypskyt", "smugl", "ulovlig", "ulovleg"]

termlist15_cc = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]  
termlist15_cc_trunc = ["art", "arter", "dyr"]                                  

termlist15_cd = ["rosewood" , "kosso" , "elephant" , "rhino" , "ivory" , "pangolin" , "turtle" , "tortoise" , "big cat" , "tiger" , "glass eel",
                 "elefant", "neshorn", "elfenbein", "elfenben", "skilpadde", "store katt", "glassål"]

termlist15_ce = ["capacity",
                 "cooperation","collaboration","support","international agreement",
                 "polic", "empower", "investing", "investment",
                 "knowledge transfer", "awareness", "knowledge", "information", "dissemination",
                 "educat", 
                 "Landscapes for People, Food and Nature partnership",
                 "Convention on International Trade in Endangered Species of Wild",
                 "anti-poach", "patrol", "detection", 
                 
                 "kapasitet", 
                 "samarbeid", "nettverk", "støtte", "stønad",
                 "politikk", "retningslin", "myndiggjør", "bistand", "ressurs",
                 "kunnskapsoverfør", "kjenner til", "kunnskap", "informasjon", "formidl",
                 "utdann",
                 "internasjonal handel med truede dyr", "internasjonal handel med truede og sårbare",
                 "anti-krypskyt", "avslør", "kontroll"]
termlist15_ce_case = ["CITES"]

phrasedefault15_ca = r'(?:{})'.format('|'.join(termlist15_ca))
phrasedefault15_cc = r'(?:{})'.format('|'.join(termlist15_cc))
phrasespecific15_cc = r'\b(?:{})\b'.format('|'.join(termlist15_cc_trunc))
phrasedefault15_cd = r'(?:{})'.format('|'.join(termlist15_cd))
phrasedefault15_ce = r'(?:{})'.format('|'.join(termlist15_ce))
phrasedefault15_ce_case = r'(?:{})'.format('|'.join(termlist15_ce_case))
```


```python
#Search 1

Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_ca, na=False, case=False))
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_cd, na=False, case=False)) 
            |(Data['result_title'].str.contains(phrasedefault15_cc, na=False, case=False))
            |(Data['result_title'].str.contains(phrasespecific15_cc, na=False, case=False))
        )
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_ce, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault15_ce_case, na=False, case=True)) # case = T
        )
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_c"] = "SDG15_c"

print("Number of results = ", len(Data[(Data.tempsdg15_c == "SDG15_c")]))  
```


```python
test=Data.loc[(Data.tempsdg15_c == "SDG15_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```python
#Termlists
termlist15_cf = ["Convention on International Trade in Endangered Species of Wild Fauna and Flora",
                 "internasjonal handel med truede dyr", "internasjonal handel med truede og sårbare arter"]
                 #Reuse 15_ce_case for CITES

termlist15_cg = ["livelihood", "employment",
                 "local communit", "local people", "indigenous communit", "indigenous people", "rural communit", "rural people", "native communit", "native people",
                 
                 "levebrød", "jobb", "tilsatt", "ansatt", "arbeid",
                 "lokale samfunn", "lokalsamfunn", "urfolk", "urbefolkning", "bygd"]

termlist15_ch = ["sustainab", "ecological", "legal", "alternativ", "eco-friendly", "environmentally friendly",
                 "bærekraft", "berekraft", "økologi", "lovlig", "lovleg", "miljøven", "økoven"]

termlist15_ci = ["fishing", "fisher", "hunting", "hunter", "touris", "agroforest", "agricult", "income",
                 "fiske", "jakt", "turism", "landbruk", "jordbruk", "inntekt"]

phrasedefault15_cf = r'(?:{})'.format('|'.join(termlist15_cf))
phrasedefault15_cg = r'(?:{})'.format('|'.join(termlist15_cg))
phrasedefault15_ch = r'(?:{})'.format('|'.join(termlist15_ch))
phrasedefault15_ci = r'(?:{})'.format('|'.join(termlist15_ci))
```


```python
#Search 1

Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault15_cf, na=False, case=False)) 
            |(Data['result_title'].str.contains(phrasedefault15_ce_case, na=False, case=True))
            |
              (
                  (Data['result_title'].str.contains(phrasedefault15_ca, na=False, case=False)) 
                  &
                  (
                      (Data['result_title'].str.contains(phrasedefault15_cc, na=False, case=False))
                      |(Data['result_title'].str.contains(phrasespecific15_cc, na=False, case=False))
                      |(Data['result_title'].str.contains(phrasedefault15_cd, na=False, case=False))
                  )
              )
        )
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_cg, na=False, case=False))
            |((Data['result_title'].str.contains(phrasedefault15_ch, na=False, case=False))&(Data['result_title'].str.contains(phrasedefault15_ci, na=False, case=False)))
          
        )
    )
    & (Data['terrestrial_double_NOT']==True)
),"tempsdg15_c"] = "SDG15_c"

print("Number of results = ", len(Data[(Data.tempsdg15_c == "SDG15_c")]))  
```


```python
test=Data.loc[(Data.tempsdg15_c == "SDG15_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15

Works mentioning SDG15


```python
#Termlists

termlist_sdg_a = ["SDG 15", "SDGs 15", "SDG15", "sustainable development goal 15", 
                  "bærekraftsmål 15", "berekraftsmål 15"]
termlist_sdg_b = ["sustainable development goal", 
                  "bærekraftsmål", "berekraftsmål"]
termlist_sdg_c = ["goal 15",
                  "mål 15"]
termlist_sdg_d = ["sustainable development goal", "SDG", "goal 15", 
                  "bærekraftsmål", "berekraftsmål", "mål 15"]
termlist_sdg_e = ["life on land", "mountain", "terrestrial", "forest", "dryland", "grassland",
                  "livet på land", "terrestrisk", "skog"]

termlist_sdg_f = ["life on land", "livet på land"]
#extra phrase where the short titles of the SDG are included, since this is a title search

phrasedefault_sdg_a = r'(?:{})'.format('|'.join(termlist_sdg_a))
phrasedefault_sdg_b = r'(?:{})'.format('|'.join(termlist_sdg_b))
phrasedefault_sdg_c = r'(?:{})'.format('|'.join(termlist_sdg_c))
phrasedefault_sdg_d = r'(?:{})'.format('|'.join(termlist_sdg_d))
phrasedefault_sdg_e = r'(?:{})'.format('|'.join(termlist_sdg_e))
phrasedefault_sdg_f = r'(?:{})'.format('|'.join(termlist_sdg_f))
```

Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 

"SDG" was also not searched for case-sensitive, as it seems to work ok without.


```python
#Search 1
Data.loc[(
      (Data['result_title'].str.contains(phrasedefault_sdg_a, na=False, case=False))
      |(Data['result_title'].str.contains(phrasedefault_sdg_f, na=False, case=False))
      |
      (
        (Data['result_title'].str.contains(phrasedefault_sdg_b, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault_sdg_c, na=False, case=False))
      )
      |
      (
         (Data['result_title'].str.contains(phrasedefault_sdg_d, na=False, case=False))
         & (Data['result_title'].str.contains(phrasedefault_sdg_e, na=False, case=False))
      )
),"tempmentionsdg15"] = "SDG15"

print("Number of results = ", len(Data[(Data.tempmentionsdg15 == "SDG15")]))  
```


```python
test=Data.loc[(Data.tempmentionsdg15 == "SDG15"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## Combine the search result labels


```python
#Examine - see new columns
test=Data.loc[Data['tempsdg15_b'].notna() & Data['tempsdg15_02'].notna()]   
test.iloc[0:4, [1,4,6,20,21,23,24, -3,-12]]
```


```python
print(Data.columns.tolist())
```


```python
# Make a copy of the data
data2=Data.copy()
```


```python
data2.info()
```


```python
#remove columns used in searching that are no longer needed
data2.drop(columns = ["terr_terms", "terrestrial_double_NOT", "marine_terms", "LDCs", "SIDS", "LDS", "LMICs", "LDCSIDS", "scp"], inplace=True)
```

### Combined target-level results
This section combines all of the target-level labels. When doing this, we also separate out those that concern the general SDG phrase (i.e. works that mention SDG4 - this is not a target, so we don't want them as a target label - your use may vary)


```python
cols_target_python=(data2.filter(like='tempsdg').columns).tolist()
print(type(cols_target_python))
```


```python
cols_mentionsthesdg_python=(data2.filter(like='tempmentionsdg').columns).tolist()
print(type(cols_mentionsthesdg_python))
```


```python
cols_target_python[0:5]
```


```python
cols_mentionsthesdg_python
```


```python
# Concatenate the labels for all the target columns
data2['SDG_target_topic_python'] = data2[cols_target_python].apply(lambda x: x.str.cat(sep=','), axis=1)
#...and all the SDG mention columns
data2['SDG_sdg_topic_python'] = data2[cols_mentionsthesdg_python].apply(lambda x: x.str.cat(sep=','), axis=1)
```


```python
test=data2.loc[Data['tempsdg15_b'].notna() & data2['tempsdg15_02'].notna()]   
#test=data2.loc[data2['tempmentionsdg02'].notna()]   
test.iloc[0:4, [1,4,6,20,21,23,24,-1,-2, -5,-14]]
```

### Combined SDG-level results


```python
data2["SDG_topic_python"]=""
```


```python
#loop to check whether the target column contains the SDG, and add that SDG to the whole SDG col
SDGlist = ["SDG01", "SDG02", "SDG03", "SDG04", "SDG07", "SDG11", "SDG12", "SDG13", "SDG14", "SDG15"]

for ei in SDGlist:
    data2["SDG_topic_python"] = np.where(data2['SDG_target_topic_python'].str.contains(ei)|data2['SDG_sdg_topic_python'].str.contains(ei), (data2["SDG_topic_python"]+","+ei), data2["SDG_topic_python"])
```


```python
#Strip beginning comma
data2["SDG_topic_python"] = data2["SDG_topic_python"].str.lstrip(',')
```


```python
#Remove the columns no longer needed
#Remove columns for each individual target...
data2.drop(columns = cols_target_python, inplace=True)
#And the columns for the whole sdg searches...
data2.drop(columns = cols_mentionsthesdg_python, inplace=True)
data2.drop(columns = "SDG_sdg_topic_python", inplace=True)
```

**How many results?**


```python
SDGlist = ["SDG01", "SDG02", "SDG03", "SDG04", "SDG07", "SDG11", "SDG12", "SDG13", "SDG14", "SDG15"]

for ei in SDGlist:
    print("No. results for", (ei), "(topic):", np.count_nonzero(data2['SDG_topic_python'].str.contains(ei)))
```


```python
SDGlist = ["SDG03_01", "SDG03_02", "SDG03_03", "SDG03_04", "SDG07_01", "SDG11_01"]

for ei in SDGlist:
    print("No. results for", (ei), "(topic):", np.count_nonzero(data2['SDG_target_topic_python'].str.contains(ei)))
```

### Final clean


```python
# Make a copy of the data
data3=data2.copy()
```


```python
#Empty SDG fields to NA
data3.loc[~data3['SDG_target_topic_python'].str.contains('SDG'), 'SDG_target_topic_python'] = np.nan
data3.loc[~data3['SDG_topic_python'].str.contains('SDG'), 'SDG_topic_python'] = np.nan
```


```python
data3.info()
```
