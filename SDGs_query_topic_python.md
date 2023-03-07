# Search queries for all currently covered SDGs - topic approach. English and Norwegian.

This file contains a method for searching for SDG relevant works within a dataset based on title (here, `result_title`). For SDG14, journal/series title (`journal`) is also used in the section "Marine terms". The script refers to an additional field, `result_id`, when displaying the results.

It currently covers SDGs 1, 2, 3, 4, 7, 11, 13, 14, and 15. This search is an adaptation of the topic searches for individual SDGs which were originally constructed in search syntax for the database Web of Science (WOS; Clarivate). A full documented version of these WOS searches can be found here https://doi.org/10.5281/zenodo.7241689. We have tried to retain a common structure between the WOS and python versions of the searches by dividing into the same "phrases" (i.e. target 1.4 phrase 2 here corresponds to target 1.4 phrase 2 in the WOS syntax searches, unless otherwise noted). Differences between the WOS and python versions are mainly:
- Adaptation to title search, rather than also being able to search in the abstract and keywords. For this reason, some searches have been simplified/broadened slightly.
- Additional language search. This file will search for SDG-related works written in both English and Norwegian. The English search terms are always provided first, with the Norwegian translated terms on a new line. By translations, we mean direct translations as well as country-specific terminology. Note that in some cases, adjustments are made to the search to deal with specifically Norwegian isses (for example, large amounts of research on salmon anaemia causing noise in a search for human anaemia); these are commented on. In documentation and notes, "(NO)" signifies it is a Norwegian search term being discussed.

The general structure of this file is 
1. Import
2. Country sets - searches to identify results mentioning certain countries, used later in searches where the targets refer to certain groups of countries.
3. Searches, split by SDG and target. Under each target, you will find the target text (English and Norwegian), any general notes, a copy of the WOS phrase used as an original starting point (these generally begin with "TS="), lists of search terms ("termlist_xx"), a search, and a preview of results. Note that occasionally, for efficiency, termlists may be re-used within a target (from an earlier phrase).
4. Code to combine all of the labels created in the above part into two columns: SDG-level results (e.g. whether a result can be related to SDG4) and target-level results (e.g. whether a result can be related to target 4.1).  
5. Cleaning

Documentation included in this file is specific to a) implementation of the search in python, b) adaptation to a title search, or c) Norwegian search terms. For documentation of original English term sources, interpretations of SDG targets, relevance choices, and contributor information, see the documentation within the original Web of Science syntax files at the doi above.

Because the Norwegian terms have been optimised to find as much SDG-related research as possible for Norway (e.g. including country-specific terminology), care should be taken if the goal of mapping publications is to compare with other countries. For that purpose, we would suggest using the Web of Science strings. 


```python
import pandas as pd
import numpy as np
```

## Import

Use file of all results, already pre-labelled with other methods if applicable. 


```python
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

LDC = least-developed countries; SIDS = small-island developing states; LDS = landlocked developing states; LMICs = Low- and middle-income countries. See WOS files for documentation and sources. 


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

```
TS=
("extreme poverty" OR "severe poverty" OR "deep poverty" OR "abject poverty" OR "absolute poverty" OR "destitution" 
OR "global poverty" OR "international poverty"
)  
```


```python
#Term lists
termlist1_1 = ["extreme poverty", "severe poverty", "deep poverty", "abject poverty", "absolute poverty", "destitution", "global poverty", "international poverty",
              "ekstrem fattigdom", "global fattigdom", "internasjonal fattigdom"
              ]

phrasedefault1_1 = r'(?:{})'.format('|'.join(termlist1_1))
```


```python
#Search 1
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


```
TS=
(
  ("anti-poverty" OR "out of poverty"
  OR "poverty" OR "rural poor" OR "urban poor" OR "working poor"
  OR (("poor" OR "poorest") NEAR/3 ("household$" OR "people" OR "communit*" OR "children" OR "relief"))
  )
  NOT "species poor"
)
```


```python
#Termlists
termlist1_2a = ["anti-poverty", "out of poverty", "poverty", "rural poor", "urban poor", "working poor",
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


```
TS=
(
  "welfare system$" OR "welfare service$" OR "social security system"
  OR "basic social service$" OR "social assistance service$" OR "social floor$"
  OR "social protection program*" OR "social insurance program*" OR "social safety net$" OR "safety net program*"
)

TS=
(
  ("social protection$" OR "social security" OR "social benefits" OR "social insurance"
  OR "basic income" OR "cash benefit$" OR "income security" OR "guaranteed income$" OR "living allowance" OR "housing assistance"
  OR "unemployment benefit$" OR "unemployment compensation" OR "unemployment insurance" OR "unemployment allowance" OR "labour market program*" OR "labor market program*" OR "public works program*"
  OR "disability benefit$" OR "disability allowance" OR "disability pension$" OR "disability tax credit$" OR "disability insurance"
  OR "health care benefit$" OR "sickness benefit$" OR "sick benefit" OR "sick pay" OR "paid sick leave" OR "paid medical leave" OR "sickness allowance"
  OR "paid matern* leave" OR "maternity pay" OR "maternity insurance" OR "maternity benefit$" OR "maternity allowance" OR "parental benefit$" OR "paid parental leave" OR "paid family leave" OR "family leave tax credit$" OR "parental leave tax credit$"
  OR "child benefit$" OR "child tax credit$" OR "child allowance"
  OR "pension$ insurance" OR "pension plan$" OR "pension benefit$" OR "public pension$" OR "state pension$"
  OR "social care service$" OR "social service$"
  )
  AND
    ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "living in poverty"
    OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
    OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
    OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
    OR (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
    OR "disabled" OR "disabilities" OR "disability"
    OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
    OR "unemployed" OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*" OR "accident$"))
    OR "women" OR "woman" OR "girls" OR "girl"
    OR "pregnant" OR "pregnancy" OR "maternity"
    OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
    OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
    OR "living with HIV" OR "living with AIDS"
    OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
    OR "indigenous group$"
    )
)
```


```python
#Termlists
termlist1_3a = ["welfare system", "welfare service", "social security", "basic social service", "social assistance service", "social floor", 
                "social protection program", "social insurance program", "social safety net", "safety net program",
                "social protection", "social benefits" , "social insurance",
                "basic income" , "cash benefit" , "income security" , "guaranteed income" , "living allowance" , "housing assistance",
                "unemployment benefit" , "unemployment compensation" , "unemployment insurance" , "unemployment allowance" , "labour market program" , "labor market program" , "public works program",
                "disability benefit" , "disability allowance" , "disability pension" , "disability tax credit" , "disability insurance", 
                "health care benefit" , "sickness benefit" , "sick benefit" , "sick pay" , "paid sick leave" , "paid medical leave" , "sickness allowance",
                "paid maternity leave" , "maternity pay" , "maternity insurance" , "maternity benefit" , "maternity allowance" , "parental benefit" , "paid parental leave" , "paid family leave" , "family leave tax credit" , "parental leave tax credit",
                "child benefit" , "child tax credit" , "child allowance",
                "pension insurance" , "pension plan" , "pension benefit" , "public pension" , "state pension",
                "social care service" , "social service", 
                
                "velferdssystem", "velferdstjeneste", "velferdsteneste", "velferdsgode", "velferdsordning", "velferdsmodell", "velferdspolitikk", 
                "folketrygd", "trygdeordning", "sikkerhetsnett", 
                "sosialpolitiske ordning", "sosialhjelp",
                "arbeidsledighetstrygd", "arbeidsløysetrygd", "alderspensjon", "uførepensjon", "sykepenger", "sjukepengar", "frikort",
                "barnetrygd", "foreldrepermisjon", "foreldrefradrag", "foreldrefrådrag"
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

```
#Phrase 1
TS= ("financial inclusion" OR "microfinanc*" OR "micro-financ*" OR "microinsurance" OR "micro-insurance" OR "microcredit" OR "micro-credit" OR "microloan$" OR "micro-loan$")
OR TS=
(
  (
    ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
    OR "ownership" OR "control" OR "right$" OR "empower*" OR "inclusion"
    OR "affordab*" OR "pro poor" OR "inexpensive" OR "free of charge" OR "free service$"
    OR "inaccessib*" OR "barrier$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*" OR "exclusion"
    OR "unaffordab*" OR "expensive"
    OR "unbanked"
    )
    NEAR/15
      ("banks" OR "a bank" OR "banking" OR "bank account$"
      OR "digital finance" OR "mobile money" OR "electronic payments" OR "digital payment$" OR "fintech"
      OR "credit" OR "savings" OR "insurance" OR "payment service$" OR "transfer service$" OR "transfer funds"
      OR (("financial" OR "monetary") NEAR/1 ("resourc*" OR "opportunit*" OR "asset*" OR "servic*"))
      )
  )

#Phrase 2
  (
    ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal"
    OR "ownership" OR "control" OR "right$"
    OR "affordab*" OR "pro poor"
    OR "empower*" OR "inclusion" OR "sharing"
    OR "tenure security" OR "secure tenure" OR "income security" OR "secure livelihood$"
    OR "inaccessib*" OR "barrier$" OR "obstacle$" OR "unequal" OR "inequalit*" OR "inequitab*"
    OR "unaffordab*" OR "exclusion" OR "land grab*" OR "insecurity"
    )      
    NEAR/5
        ("economic resource$" OR "employment" OR "decent work" OR "paid work" OR "labour market$"
        OR "income" OR "livelihood$" OR "wealth" OR "inheritance"
        OR "land" OR "lands" OR "farmland$" OR "property" OR "natural resource$" OR "tenure"
        )
  )

#Phrase 3
  (
    ("access*" OR "equitab*" OR "equity" OR "equality" OR "equal" OR "empower*" OR "inclusion"
    OR "ownership" OR "right$"
    OR "affordab*" OR "inexpensive" OR "low cost" OR "pro poor" OR "free of charge" OR "free service$"
    )
    NEAR/10
        (
          ("basic" NEAR/2 ("service$" OR "facility" OR "facilities"))
        OR
          (("drinking water" OR "sanitation" OR "hygiene" OR "toilet" OR "handwashing" OR "hand-washing" OR "sewage" OR "WASH")
          NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "safe")
          )
        OR "improved drinking water" OR "improved source$ of drinking water" OR "clean drinking water" OR "clean water"
        OR (("waste" OR "garbage" OR "rubbish") NEAR/2 ("service$" OR "facility" OR "facilities"))
        OR (("health" OR "medical") NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "essential" OR "primary" OR "care"))
        OR "healthcare"
        OR (("education*" OR "school*") NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "primary"))
        OR
          (("basic information" OR "telecommunication" OR "basic communication" OR "ICT")
          	NEAR/2 ("service$" OR "facility" OR "facilities" OR "infrastructure")
          )
        OR "electricity service$" OR "energy service$" OR "modern energy" OR "clean fuel$" OR "clean energy"
        OR "public open space$" OR "public space$"
        OR "basic mobility" OR "urban mobility" OR "rural mobility" OR "all-season road$"
        OR ("transport*" NEAR/2 ("service$" OR "infrastructure" OR "system$" OR "public"))
        )
  )

  AND
    ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "living in poverty"
    OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
    OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
    OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
    OR (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
    OR "disabled" OR "disabilities" OR "disability"
    OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
    OR "unemployed" OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*" OR "accident$"))
    OR "women" OR "woman" OR "girls" OR "girl"
    OR "pregnant" OR "pregnancy" OR "maternity"
    OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
    OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
    OR "living with HIV" OR "living with AIDS"
    OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
    OR "indigenous group$"
    OR "least developed countr*" OR "least developed nation$" OR "Angola*" OR "Benin" OR "beninese" OR "Burkina Faso" OR "Burkina fasso" OR "burkinese" OR "burkinabe" OR "Burundi*" OR "Central African Republic" OR "Chad" OR "Comoros" OR "comoro islands" OR "iles comores" OR "Congo" OR "congolese" OR "Djibouti*" OR "Eritrea*" OR "Ethiopia*" OR "Gambia*" OR "Guinea" OR "Guinea-Bissau" OR "guinean" OR "Lesotho" OR "lesothan*" OR "Liberia*" OR "Madagasca*" OR "Malawi*" OR "Mali" OR "malian" OR "Mauritania*" OR "Mozambique" OR "mozambican$" OR "Niger" OR "Rwanda*" OR "Sao Tome and Principe" OR "Senegal*" OR "Sierra Leone*" OR "Somalia*" OR "South Sudan" OR "Sudan" OR "sudanese" OR "Togo" OR "togolese" OR "tongan" OR "Uganda*" OR "Tanzania*" OR "Zambia*" OR "Cambodia*" OR "Kiribati*" OR "Lao People’s democratic republic" OR "Laos" OR "Myanmar" OR "myanma" OR "Solomon islands" OR "Timor Leste" OR "Tuvalu*" OR "Vanuatu*" OR "Afghanistan" OR "afghan$" OR "Bangladesh*" OR "Bhutan*" OR "Nepal*" OR "Yemen*" OR "Haiti*"
    )
)
```

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
    | ((Data['result_title'].str.contains(phrasedefault1_4b, na=False, case=True)) & (Data['result_title'].str.contains(phrasedefault1_4c, na=False, case=True)))
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
                "lønnet arbeid", "løna arbeid", "anstendig arbeid.*", "arbeidsmark.*", "inntekt", "løn", "levebrød", "underhold", "underhald", "rikdom", "arv", "arving",
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
    ) & (~Data['result_title'].str.contains(phrasedefault1_4g, na=False, case=False))
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

Here under terms for indigenous and minorities, we have included Norwegian-specific groups (Sami people and Norwegian official minorities (source: Utdanningsdirektoratet (n.d.) Nasjonale minoriteter. https://www.udir.no/laring-og-trivsel/nasjonale-minoriteter/hva-er-en-nasjonal-minoritet/ (accessed Nov 2022)))


```
TS=
(
  (
    ("protect*" OR "safeguard*"  
    OR "safety net$" OR "social protection$" OR "social floor$" OR "social security"
    OR "coping" OR "cope" OR "adapt*" OR "resilien*" OR "mitigat*" OR "preparedness" OR "protection" OR "early warning"
    OR "impact$" OR "vulnerab*" OR "exposure"
    OR
      (
        ("disaster$" OR "risk$")
        NEAR/3
            ("plan" OR "plans" OR "planning" OR "strateg*" OR "reduc*" OR "relief"
            OR "manag*" OR "program$" OR "programme$" OR "policy" OR "policies" OR "medical response$"
            )
      )
    OR "Sendai"
    )
    NEAR/15
        ("disaster$" OR "catastrophe$"
        OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
        OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
        OR "drought$" OR "flood*"
        OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
        OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
        OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
        OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
        OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
        OR (  
              ("anthropogenic" OR "natural" OR "climat*"
              OR "environmental" OR "deforestation" OR "desertification" OR "degredation" OR "pollution" OR "erosion"
              OR "chemical" OR "heavy metal$" OR "pesticide$"
              OR "biological" OR "disease" OR "zoonotic"
              OR "technological" OR "radioactive" OR "nuclear" OR "cyber" OR "industrial" OR "construction" OR "transportation"
              )
              NEAR/3 ("hazard$")
           )
        OR "outbreak$" OR "pandemic$" OR "epidemic$"
        OR "war" OR "wars" OR "armed conflict$"
        OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
        OR "financial crash*" OR "financial shock$" OR "financial disaster$"
        OR "economic downturn$" OR "economic shock$" OR "economic disaster$"
        )
  )
  AND
      ("poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "living in poverty"
      OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*" OR "neighbo$rhood*"))
      OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
      OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
      OR (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
      OR "disabled" OR "disabilities" OR "disability"
      OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
      OR "unemployed" OR (("work" OR "workplace" OR "worker$" OR "occupational") NEAR/3 ("injury" OR "injuries" OR "illness*" OR "accident$"))
      OR "women" OR "woman" OR "girls" OR "girl"
      OR "pregnant" OR "pregnancy" OR "maternity"
      OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
      OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
      OR "living with HIV" OR "living with AIDS"
      OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
      OR "indigenous group$"
      OR ***least developed countries***
    )  
)

```


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
                "disadvantaged", "marginalis", "marginalized", "vulnerable", "discriminated",
                "slum", "shanty town", "informal settlement", "homeless",
                "patient", "disabled", "disabilities", "disability",
                "older people", "old people", "retired people", "elderly", "elders", "pensioner", 
                "unemployed",
                "women", "woman", "girl", "pregnan", "maternity", "child", "baby", "babies", "newborn", "toddler", "youth", "infant",
                "indigenous", "minorities", "minority", "refugee", "asylum", "immigrant",
                "trans people", "transgender", "lgbt", "lesbian", "gay", "bisexual", "intersex",
 
                "fattig", "lavinntekt", "lav inntekt", "låginntekt", "låg inntekt",
                "sårbar", "diskrimin",
                "hjemløs","heimlaus",
                "pasient", "uføre", "funksjonshem",
                "eldre", "de gamle", "dei gamle",
                "arbeidsløs","arbeidslaus",
                "kvinne", "jente", "gravid", "barn", "born", "babier", "nyfødt","nyfødd",
                "urfolk", "urinnvånarar", "urbefolkning", "urinnvånere", "sápmi", "sami", "minoritet", "jøder", "jådar", "kvener", "kvenar", "norskfinn", "skogfinn", "romani", "tatere", "taterar", "asylsøk", "flyktning", "innvandrer", "innvandrar",
                "transperson", "lesbisk", "homofile", "bifile", "lbht", "interkjønn",
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


```
TS=
(
  (
    ("ODA" OR "development spending" OR "cooperation fund"
    OR  (
          ("international" OR "development" OR "foreign")
          NEAR/3
              ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
              OR "aid" OR "assistance"
              OR "fund$" OR "funding" OR "grant$" OR "investment$" OR "investing" OR "financing" OR "financial support" OR "financial resources" OR "capital flow$"
              )
        )    
    )
    NEAR/15 ("anti-poverty" OR "out of poverty" OR "pro poor" OR "poverty")
  )
  AND
      (****LMICs****
      )
)
```

Here a change in structure is suggested - as this is a title search, a simplification, where some terms count as relevant without needing to mention "poverty". While a work about "cooperation" would still need to mention "poverty", works are included if terms such as "official development aid" (termlist_aaalt) are in the title.


```python
#Termlists
termlist1_aa = ["oda", "development spending", 
                "aid", "assistance", "funding", "grant", "invest", "investment.*", "investing", "financial support", "financing", "resources", "capital flow",
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
termlist1_aaalt2 = ["aid", "assistance", "funding", "grant", "invest", "investment.*", "investing", "financial support", "financing", "resources", "capital flow",
                    "cooperation", "co-operation", "collaboration.*", "network.*", "partnership.*"
                    "midlar", "økonomiske ressurs.*", "finansiel.*", "ressurs.*", "investering", "nødhjelp", "naudhjelp","kapitalstrøm",              
                    "samarbeidsfond.*", "samarbeid.*", "nettverk", "partnerskap.*", "partnarskap.*"
                   ]

termlist1_ab = ["poverty", "pro-poor",
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
test.iloc[0:5, ]
```

### SDG 1.b

*1.b Create sound policy frameworks at the national, regional and international levels, based on pro-poor and gender-sensitive development strategies, to support accelerated investment in poverty eradication actions*

*Opprette gode politiske rammeverk på nasjonalt, regionalt og internasjonalt nivå basert på utviklingsstrategier som gagner de fattige og ivaretar kjønnsperspektivet, med sikte på å øke investeringer i tiltak som bekjemper fattigdom*

```
TS=
(
  ("law$" OR "legislat*"
  OR "program*" OR "strateg*" OR "policy" OR "policies" OR "plan" OR "framework$" OR "initiative$"
  OR "investment policy" OR "investment policies"
  )
  NEAR/15
      ("anti-poverty" OR "out of poverty" OR "pro poor"
      OR  ("poverty"
          NEAR/3
              ("minimi*" OR "reduc*" OR "mitigat*"
              OR "alleviat*" OR "tackl*" OR "fight*" OR "combat*"
              OR "end" OR "ending" OR "eliminat*" OR "eradicat*" OR "prevent*"
              OR "lift out of" OR "lifting out of" OR "overcom*" OR "escap*" OR "relief"  
              )
          )
      )
)
```


```python
#Termlists
termlist1_ba = ["legislat", "program", "strateg", "policy", "policies", "planning", "framework", "initiativ",
                "lovverk", "lovgiv", "politikk", "retningslinje", "utredning", "utgreiing", "rammeverk", "tiltaksplan", "planer", "planar"]
termlist1_ba_trunc = ["law", "laws", "plan", "plans"]

termlist1_bb = ["anti poverty", "anti-poverty", "antipoverty"]

termlist1_bc = ["poverty", 
                "fattig"
                ]

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

```
TS=
("SDG 1" OR "SDGs 1" OR "SDG1" OR "sustainable development goal$ 1"
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 1")
    NEAR/50 "poverty"
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
```


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

```
#Phrase 1
TS=
(
  ("end hunger" OR "ending hunger" OR "ends hunger" OR "world hunger"
  OR "hunger and poverty" OR "poverty and hunger" OR "famine$"
  OR "food insecurity" OR "nutritional insecurity"
  )
  NOT (("feast and famine" OR "feast-famine") NOT ("end* hunger" OR "malnutrition"))    
)

#Phrase 2
TS=
(
  "right to food" OR "right to adequate food" OR "food sovereignty"
  OR "nutrition* security" OR "nutrition* quality" OR "nutrition sensitive agriculture"
  OR ("food" NEAR/5 ("access" OR "safety" OR "unsafe" OR "secure" OR "security" OR "reliable" OR "reliability"))
)

#Phrase 3
TS=
 (
    ("food supply" OR "nutritional value" OR "nutrient content" OR "nutritional content")  
    AND
        ("humans" OR "humanity" OR "human" OR "people" OR "person$"
        OR "children" OR "child" OR "under fives" OR "infant$" OR "toddler$" OR "babies" OR "teenager$" OR "adolescent$" OR "youth$" OR "girls" OR "boys"
        OR "adult$" OR "women" OR "men" OR "woman" OR "man"
        OR "agricultur*" OR "food security" OR "poverty"
        OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali$ed group" OR "marginali$ed groups" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
        OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
        OR "rural" OR "urban" OR "countr*" OR "nation$" OR "develop* state$"
        )
)
```

#### Phrase 1


```python
#Term lists
termlist2_1a = ["end hunger", "ending hunger", "ends hunger", "world hunger", "hunger and poverty", "poverty and hunger", "famine",
               "food insecurity", "nutritional insecurity",
                
               "utrydde sult", "utrydde svolt", "utrydje svolt", "utrydda svolt", "utrydja svolt", "bekjempe sult", "bekjempe svolt", 
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
                "nutrition security", "nutritional security", "nutritional quality", "nutrition sensitive agriculture",
                "access to food", "food access", "food safety", "safe food", "food security",
                
                "tilgang til mat", "matforsyning",
                "nok mat",  "tilstrekkelig mat", "trygg mat", "sunn mat", "sunne mat", "matsikkerhet"
              ]
              
termlist2_1c = ["Norwegian Scientific Committee for Food Safety"]
#This term list is specific for Norway and can be dropped for works from other countries.
#There are lots of reports from VKM Norwegian Scientific Committee for Food Safety found in this string. 
#These are mostly very specialised, for example risk assessments of certain substances. Therefore removed for now, but this could be discussed.
#Note that this does not remove all VKM reports, but does exclude those with "opinion of the Norwegian..." in the title. A number of more general reports from VKM are still there.

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

termlist2_1d = ["food supply", "nutritional value", "nutrient content", "nutritional content", 
                "næringsinnhold", "næringsinnhald"
              ]
              #We did include "næringstoff"(NO), but nearly all results were about leaching of nutrients into water bodies, and not about human nutrition

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

```
#Phrase 1
TS=
(
  ("malnutrition" OR "malnourish*"
  OR "kwashiorkor" OR "marasmus"
  OR "anaemia" OR "anemia"
  OR
    (
      ("deficien*" OR "inadequa*")
      NEAR/3
          ("nutritional" OR "dietary" OR "vitamin$" OR "micronutrient$" OR "iron" OR "iodine")
    )
  OR  
    (
      ("stunting" OR "stunted" OR "wasting" OR "underweight")
      NEAR/15 ("child*" OR "infant$" OR "under five$" OR "babies" OR "toddler$" OR "girl$" OR "boy$")
    )
  OR "obesity" OR "overweight" OR "obese"
  )
  NOT ("salmon anemia")    
)

#Phrase 2
TS=
(
  ("nutritio*" NEAR/5 ("access" OR "safe" OR "unsafe" OR "secure" OR "reliable" OR "reliability"))
  OR "diet* quality" OR "nutrition* security" OR "nutrition* quality" OR "nutrition sensitive agriculture"
  OR
    (
      ("nutritio*" OR "folate status" OR "micronutrient$")
      NEAR/5
          ("women" OR "mother$" OR "pregnancy"
          OR "child*" OR "under five$" OR "infant$" OR "toddler$" OR "girl$" OR "boy$" OR "babies" OR "perinatal"
          OR "old* persons" OR "old* people" OR "elderly" OR "older adult$"
          )
    )
)

#Phrase 3
TS=
(
  ("protein deficiency"
  OR "undernourish*" OR "under-nourish*" OR "undernutrition" OR "under-nutrition"
  )
  AND
      ("humans" OR "humanity" OR "human" OR "people" OR "person$"
      OR "children" OR "child" OR "under fives" OR "infant$" OR "toddler$" OR "babies" OR "teenager$" OR "adolescent$" OR "youth$" OR "girls" OR "boys"
      OR "adult$" OR "women" OR "men" OR "woman" OR "man"
      OR "agricultur*" OR "food security" OR "poverty"
      OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
      OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
      OR "rural" OR "urban" OR "countr*" OR "nation$" OR "develop* state$"
      )
)

```

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
                "overvekt", "fedme"
              ]

termlist2_2b = ["stunting", "stunted", "wasting", "underweight",
                "veksthemm", "avmagring", "undervekt"       
              ]

termlist2_2c = ["child", "infant", "under five", "under-five", "babies", "baby", "toddler", "girl", "boy",
                "barn", "jenter", "gutter", "gutar"
              ]

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

                "næringssikkerhet", "næringskvalitet", "tilgang til næring", "trygg næring"
              ]

termlist2_2e = ["nutrition", "folate", "micronutrient",
                "ernæring", "næringsstoff", "næringsrik", "folsyre", "folacin", "folat", "mikronæring"
                ]

termlist2_2f = ["child", "infant", "under five", "under-five", "babies", "baby", "toddler", "girl", "boy", "perinatal", "prenatal",
                "older person", "old person", "old people", "elderly", "older adult",
                "women", "mother", "pregnan",

                "barn", "jenter", "gutter", "gutar",
                "gammel person", "eldre", "de gamle",
                "kvinne", "gravid"
              ]
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
        & ((Data['result_title'].str.contains(phrasedefault2_2e, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault2_2f, na=False, case=False)))
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
termlist2_2h = ["undernutrition", "under-nutrition", "undernourish", "protein deficien", 
                "underernær", "proteinmangel"
              ]

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

```
  TS=
  (
    (
      ("intensification" NEAR/5 ("smallhold*" OR "sustainable" OR "agroecolog*" OR "ecolog*"))  
      OR "production" OR "productivity" OR "yield$" OR "agricultural output$" OR "farm output$"
      OR "livelihood$" OR "income$" OR "profit*" OR "revenue" OR "economic viability"
      OR "value addition" OR "diversification" OR "non-farm employment" OR "off-farm employment" OR "off farm income"
      OR "access*" OR "empowerment" OR "benefit$" OR "tenure"
      OR ("right$" NEAR/5 ("farmland$" OR "land" OR "property" OR "tenure"))
      OR "equity" OR "equitable" OR "justice" OR "injustice"
      OR "barrier$" OR "obstacle$"
      OR "land grab*" OR "tenure insecurity"
      )
      AND
          ("smallhold*" OR "family farm*" OR "family run farm*" OR "family owned farm*" OR "home gardening"
          OR
            (
              ("small-scale" OR "indigenous" OR "homestead*" OR "subsistence")
              NEAR/5
                (
                  ("food producer$" OR "food production" OR "food grower$" OR "agro food$"
                  OR "agricultur*" OR "farm*" OR "permaculture"
                  OR "cropping system$" OR "orchard$" OR "arable land$"
                  OR "pasture$" OR "pastoral*" OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
                  OR "aquaculture" OR "fisher*" OR "fish farm*"
                  )
                OR
                  (
                    ("crop$" OR "produce" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
                    OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
                    )
                    NEAR/5
                        ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding")
                  )
                )
            )
          )
)
```


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
                "sysselsette utanfor", "sysselsetting utanfor"
                "tilgang", "myndiggjør", "fordel", "eierskap", "eigarskap"
                "landrett",  "rettigheter til land", "eiendomsrett", "eigedomsrett", "landrike", "landfattig", "jordleie",
                "likestilling", "ulikhet", "ulikskap", "rettferd", "rettighet", "ekskludering", "marginali"
              ]
              #I have added ownership and production resources here. "tilgang/access" (NO) will cover access to land, knowledge, financial services etc.

termlist2_3b = ["smallhold", "family farm", "family run farm", "family owned farm", "home gardening",
                "småbruk", "familiegård", "familiegard", "familiebruk", "kjøkkenhage", "grønnsakshage", "reindrift", "husdyrnomad"
                ]
                #"reindrift" (NO, reindeer herding) added, often small-scale.

termlist2_3c = ["small-scale", "indigenous", "homestead", "subsistence",
                "småskal", "urfolk", "urbefolk", "sami", "sapmi", "samer", "subsistens"
                ]
                #"Sami" was added as an indigenous group relevant for Norway. "Sami" will cover "samisk" (NO)

termlist2_3d = ["food-produc", "food produc", "grower", "agro food", "agri-food", "agro-food",
                "agricultur", "farm", "permacultur", "cropping", "orchard", "arable land",
                "pasture", "pastoral", "agroforest", "agro-forest", "silvopastur", "silvopastoral",
                "aquacultur", "fisher", "fish farm", "herding",
                "crop", "grain", "vegetable", "fruit", "cereal", "rice", "wheat", "maize", "pulses", 
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matproduksjon", "matprodusent",
                "gård", "gard", "landbruk", "jordbruk", "gårdsbruk", "gardsbruk", "dyrket mark", "dyrkamark", "dyrka mark", "kultivert mark",
                "beite", "dyreproduksjon", "meieri",
                "fiskeoppdrett", "lakseoppdrett",
                "grønnsak", "grønsak", "frukt", "fisk", "laks", "sau", "storfe", "svin", "fjærkre", "rein"
                ]
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
```
TS=
(
  (
      ("food production" OR "food grower$"
      OR "farm*" OR "agricultur*" OR "ecoagricultur*" OR "eco agricultur*" OR "permaculture"
      OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
      OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
      OR "aquaculture" OR "fish farm*"
      OR
        (
          ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
          OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
          )
          NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
        )      
      )
      NEAR/15
          ("intensification" OR "production" OR "productivity" OR "efficiency" OR "yield$" OR "agricultural output$" OR "farm output$")  
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*")
)
```


```python
#Termlists
termlist2_4a = ["food-produc", "food produc", "grower", "agro food", "agri-food", "agro-food", 
                "agricultur", "farm", "smallhold", "permacultur", "cropping", "orchard", "arable land",
                "pasture", "pastoral", "agroforest", "agro-forest", "silvopastur", "silvopastoral",
                "aquacultur", "fisher", "fish farm", "herding",
                "crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", 
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matproduksjon", "matprodusent",
                "gård", "gard", "landbruk", "jordbruk", "gårdsbruk", "gardsbruk", "småbruk", "familiebruk", "dyrket mark", "dyrkamark",
                "dyrka mark", "kultivert mark",
                "beite", "dyreproduksjon", "meieri",
                "fiskeoppdrett", "lakseoppdrett",
                "grønnsak", "grønsak", "frukt", "fiske", "laks", "sau", "storfe", "svin", "fjærkre", "rein"
                ]
                #I put a space before " rice" to avoid "price". Note that "agricultur" will also cover e.g. "ecoagriculture"

termlist2_4b = ["intensif", "productivity", "efficiency", "yield", "agricultural output", "farm output",
                "produktivitet", "effektivitet", "avling"
                ]

termlist2_4c = ["production", "produksjon"]

termlist2_4d = ["increas", "improv",
                "økt", "øke", "auke", "auka"
                ]
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
```
TS=
(
  (
      ("food production" OR "food grower$" OR "agro food"
      OR "farm*" OR "agricultur*" OR "ecoagricultur*" OR "eco agricultur*" OR "permaculture"
      OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoralist$"
      OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
      OR "aquaculture" OR "fisher*" OR "fish farm*"
      OR "crop$" OR "cereal$" OR "rice" OR "wheat" OR "maize"
      OR "livestock" OR "cattle" OR "sheep" OR "poultry" OR "chicken$" OR "pig$" OR "goat$"
      OR
        (
          ("grain$" OR "vegetable$" OR "fruit$" OR "pulses" OR "fish" OR "buffalo*" OR "duck$")
          NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
        )      
      )
      NEAR/15
            ("climate smart agriculture" OR "resilien*"
            OR (("disaster$" OR "risk$") NEAR/3 ("plan*" OR "strateg*" OR "relief" OR "manag*"))
            OR "vulnerability"
            )  
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*" OR "wild pig$")
)
```


```python
#Termlists
termlist2_4e = ["climate smart", "climate-smart", "resilien", "vulnerability", 
                "disaster plan", "disaster management", "disaster strateg", "disaster relief", "risk plan", "risk management", "risk strate", "risk reduction", "manage risk"
                
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
```
TS=
(
  (
      ("food production" OR "food grower$" OR "agro food"
      OR "farm*" OR "agricultur*" OR "ecoagricultur*" OR "eco agricultur*" OR "permaculture"
      OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoralist$"
      OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
      OR "aquaculture" OR "fisher*" OR "fish farm*"
      OR "crop$" OR "cereal$" OR "rice" OR "wheat" OR "maize"
      OR "livestock" OR "cattle" OR "sheep" OR "poultry" OR "chicken$" OR "pig$" OR "goat$"
      OR
        (
          ("grain$" OR "vegetable$" OR "fruit$" OR "pulses" OR "fish" OR "buffalo*" OR "duck$")
          NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
        )      
      )
      NEAR/15
          (
            ("adapt*" OR "mitigat*" OR "protect*" OR "avoid*" OR "limit" OR "prevent*"
            OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
            OR "cope" OR "coping" OR "tolera*" OR "preparedness" OR "early warning"
            )
            NEAR/5
                ("climate change" OR "climatic change$" OR "global warming" OR "changing climate"
                OR "disaster$" OR "catastroph*"
                OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
                OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
                OR "drought$" OR "flood*"
                OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
                OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
                OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
                OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
                OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
                OR "tipping point$"  
                OR "outbreak$" OR "pandemic$" OR "epidemic$"
                OR "war" OR "wars" OR "armed conflict$"
                OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
                OR "financial crash*" OR "financial shock$" OR "financial disaster$"
                OR "economic downturn$" OR "economic shock$" OR "economic disaster$"
                )
          )
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*" OR "wild pig$")
)
```


```python
#Termlists
termlist2_4f = ["adapt", "mitigat", "protect", "avoid", "limit", "prevent", "manag", 
                "planning", "plans", "strateg", "disaster reduc", "risk reduc", "relief", "program", "programme", "policy", "policies", "strateg", "framework", "governance", "legislat",
                "cope", "coping", "tolera", "preparedness", "early warning",
                "sendai",

                "tilpass", "forbered", "førebu", "beskytt", "unngå", "begrens", "hindr", "forebygg", "førebygg" ,"håndter",
                "planer", "planlegging", "handlingsplan", "rammeverk", "politikk", "retningslin", "styring", "ledelse", "leiing", "lovgiv", 
                "katastrofeplanlegging", "risikoreduksjon", "strategi", "krisehåndtering", 
                "tåle", "beredskap", "varsling", "varsel"                
                ]
              
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
                 "finanskatastrofe", "finanskræsj", "økonomisk nedgang", "økonomisk sjokk", "økonomisk katastrofe"
                ] 
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
The following report from NIBIO was used to help with Norwegian sustainable agriculture terms https://nibio.brage.unit.no/nibio-xmlui/bitstream/handle/11250/2638984/NIBIO_RAPPORT_2020_6_4.pdf?sequence=1&isAllowed=y

```
TS=
  ("ecoagricultur*" OR "eco-agricultur*" OR "permaculture"
  OR "conservation agriculture" OR "conservation farming"
  )
OR
TS=
(
  (
    ("food production" OR "food grower$" OR "agri food"
    OR "farm*" OR "agricultur*"
    OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
    OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
    OR "aquaculture" OR "fisher*" OR "fish farm*"
    OR
      (
        ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
        OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
        )
        NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
      )      
    )
    NEAR/15
        ("sustainab*" OR "agroecolog*" OR "eco-friendly" OR "environmentally friendly" OR "ecosystem approach"
        OR ("organic" NEAR/3 ("farm*" OR "agricultur*" OR "cultivation" OR "gardening" OR "production" OR "orchard$" OR "pasture$" OR "aquaculture"))
        OR "natural pest control" OR "natural pest management" OR "biological pest control" OR "intergrated pest management"
        OR "intercropping" OR "cover crop$" OR "crop rotation" OR "polyculture$" OR "permaculture"
        OR "reduced tillage" OR "mulch" OR "mulching"
        OR "water conservation"       
        )   
  )
  NOT ("solar farm*" OR "wind farm*" OR "power farm*")  
)
```


```python
#Termlists
termlist2_4i = ["ecoagricultur", "eco-agricultur", "agroecolog", "permaculture", "conservation agriculture", "conservation farming",
                "organic farm", "organic agricult", "organic crop", "organic orchard", "organic arable", "organic pasture",
                "organic aquacultur", "organic salmon", "organic pig", "organic poultry", "organic dairy", "organic reindeer",

                "økolandbruk", "økojordbruk", "permakultur"           
                ]
                #"organic" is not used alone, but is instead combined in phrases to avoid e.g. organic acids, organic matter. Moved to this part rather than 4j as it can stand alone.
              
termlist2_4j = ["sustainab", "eco-friendly", "environmentally friendly", "ecosystem approach",
                "natural pest control", "natural pest management", "biological pest control", "intergrated pest management",
                "intercropping", "cover crop", "crop rotation", "polyculture", "permaculture", 
                "reduced tillage", "mulch", "mulching",
                "water conservation",

                "bærekraftig", "berekraftig", "selvbærende", "sjølvberande", "miljøvennlig", "miljøvennleg", "miljøvenleg", "miljøbevisst", 
                "miljømedveten", "miljømedviten", "økosystem", "økologisk", "biologisk bekjempelse", "biologisk nedkjemping", "biologisk skadedyrkontroll", 
                "integrert skadedyrkontroll", "integrert ugrasbekjempelse", "integrert plantevern",
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
The following NIBIO report was used to help with relevant Norwegian terms around soil management: https://hdl.handle.net/11250/2738064

```
TS=
(
    ("food production" OR "food grower$" OR "agri food"
    OR "farm*" OR "agricultur*" OR "permaculture"
    OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
    OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
    OR "aquaculture" OR "fisher*" OR "fish farm*"
    OR
      (
        ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
        OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
        )
        NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
      )      
    )
    NEAR/15
          ("soil conservation"
          OR "soil structure" OR "soil fertility" OR "soil health"
          OR ("quality" NEAR/5 ("soil" OR "land" OR "farmland"))
          OR "biodiversity" OR "agrobiodiversity" OR "species diversity" OR "ecosystem$" OR "pollinator$"
          )     
)
```


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
The following NIBIO report was used to help with relevant Norwegian terms around soil management: https://hdl.handle.net/11250/2738064

```
TS=
(
  ("food production" OR "food grower$" OR "agri food"
  OR "farm*" OR "agricultur*" OR "permaculture"
  OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$" OR "pastoral*"
  OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
  OR "aquaculture" OR "fisher*" OR "fish farm*"
  OR
    (
      ("crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
      OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
      )
      NEAR/5 ("production" OR "producer$" OR "grower$" OR "herder$" OR "herding" OR "ranch*" OR "plantation$")
    )      
  )
  NEAR/15
      ("desertification"
      OR
        ("soil$"
        NEAR/5
            ("loss" OR "degradation" OR "depletion" OR "nutrient imbalance$"
            OR "erosion" OR "compaction" OR "waterlogging"
            OR "salinization" OR "salinisation" OR "acidification"
            OR "chemical pollution" OR "contamination"
            )
        )
      OR
        (
          ("ecosystem$" OR "biodiversity" OR "land" OR "species" OR "pollinator$")
          NEAR/5 ("loss" OR "degradation" OR "depletion")
        )
      )
)
```


```python
#Termlists
#Note that we don't need biodiversity/pollinator terms here because they are already covered in phrase 5
termlist2_4l = ["desertification", "land degradation",
                "vannknapphet", "ørkenspredning", "ørkenspreiing", "forørkning", "landforringelse", "jordforringelse"]

termlist2_4m = ["soil", "cropland", "farmland", "arable land", "cultivated land", "agricultural land",
                "jord", "dyrket mark", "dyrka mark", "dyrkamark", "dyrket land", "dyrka land"
                ]
                #"land" had some noise if used alone, for example "Greenland"

termlist2_4n = ["loss", "degradation", "depletion", "erosion", "compaction", "waterlogging", "salinization", "salinisation", "acidifi", "pollut", "contaminat",
                "forring", "forverr", "næringsfattig", "avrenning", "jordtap", "erosjon", "forsalting", "jordpakking", "forsuring", "forurensing", "forureining"
                ]

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
```
#Phrase 1
TS=
(
    "plant genetic resource$" OR "animal genetic resource$"
    OR  
      (
        ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
        NEAR/3 ("breed$" OR "cultivar$")
      )
    OR "agricultural diversity" OR "agricultural biodiversity" OR "agrobiodiversity"
    OR  
      (
        (
          ("local" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
          NEAR/1 
            ("variet*" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
            OR "livestock" OR "poultry" OR "cattle" OR "sheep" OR "goat$" OR "chicken$" OR "duck$" OR "buffalo*")
        )
        AND "agricult*"
      )
    OR
      ("landrace$"
      NEAR/5
        ("maintain*" OR "conserv*" OR "preserv*" OR "protect*"
        OR "diversity" OR "genomic variation" OR "genetic variation"
        OR "loss" OR "extinction" OR "declin*" OR "disappear*"
        )    
      )    
)

#Phrase 2
TS=
(
        ("genetic diversity" OR "genetic resource$"
        )
        NEAR/15
            ("agricultur*" OR "domestic*" OR "farming" OR "farm$" OR "farmer$" OR "cultiva*" OR "permaculture"
            OR "cropping system$" OR "orchard$"
            OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
            OR "aquaculture"
            OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
            OR "livestock" OR "poultry" OR "cattle" OR "sheep" OR "pig$" OR "goat$" OR "chicken$" OR "duck$" OR "buffalo*"
            OR "landrace$" OR "wild relative$"
            OR
              (
                ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
                NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
              )
            )
)
```


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
                "ville slekt",      
                "gamle eplesort", "gamle eplevariant", "tradisjonelle eplesort", "tradisjonelle eplevariant"       
                ]
                #Apples are added in Norwegian as this seems to be a specific focus area

termlist2_5b = ["heirloom", "wild relative", "genetic resource","genetic diversity",
                "mangfold", "mangfald", "ville", "viltvoks", "viltvaks", "tradisjonelle", "genetiske ressurs", "genressurs", "genetikk diversit"
                ]

termlist2_5c = ["food-produc", "food produc", "grower", "agro food", "agri-food", "agro-food", 
                "agricultur", "farm", "smallhold", "permacultur", "cropping", "orchard", "arable land",
                "pasture", "pastoral", "agroforest", "agro-forest", "silvopastur", "silvopastoral",
                "aquacultur", "fisher", "fish farm", "herding",
                "crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", 
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matproduksjon", "matprodusent",
                "landbruk", "jordbruk", "gårdsbruk", "gardsbruk", "småbruk", "familiebruk", "dyrket mark", "dyrkamark", "dyrka mark", "kultivert mark",
                "beite", "dyreproduksjon", "meieri",
                "fiskeoppdrett", "lakseoppdrett",
                "grønnsak", "grønsak", "frukt", "laks", "sau", "storfe", "svin", "fjærkre", "rein",
                "eplesort", "epler", "epledyrk"
                ]
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
test.iloc[0:5, ]
```

#### Phrase 3

Here we have simplified (to adapt from abstract to title search) - drop the terms starting `"diversity" OR "genetic resources"...` so it is enough for the title to mention cryoconservation / genebanks. In the abstract the more detialed approach was necessary becaue many works mention that they *used* a gene bank in the methods, but are not about gene banks. 

```
TS=
(
  (
      ("cryoconservation"
      OR
        (
          ("plant bank$" OR "seed bank$"
          OR "gene bank$" OR "genebank$" OR "germplasm bank$" OR "cryobank$"
          OR "ex situ" OR "cryopreserv*"
          )
          NEAR/15
              ("diversity" OR "genetic resources" OR "agricultural biodiversity"
              OR "maintain*" OR "conserv*" OR "preserv*" OR "protect*" OR "extinct*" OR "endangered"
              OR "collection$ management" OR "collection$ development"
              OR "funding" OR "fund" OR "invest" OR "investing" OR "investment$"
              OR "plan" OR "planning" OR "plans" OR "policy" OR "policies" OR "strateg*" OR "framework$" OR "governance" OR "legislat*"
              )
        )
      )  
      NEAR/15
          ("agricultur*" OR "farming" OR "farm$" OR "farmer$" OR "cultiva*" OR "permaculture"
          OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$"
          OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
          OR "aquaculture"
          OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
          OR "livestock" OR "poultry" OR "cattle" OR "sheep" OR "pig$" OR "goat$" OR "chicken$" OR "duck$" OR "buffalo*"     
          OR "landrace$" OR "wild relative$"
          OR
            (
              ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
              NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
            )
          )
  ) NOT ("soil seed bank$" OR "weed seed bank$" OR "dung seed bank$")        
)
```


```python
#Termlists
termlist2_5d = ["cryoconserv", 
                "kryo-bevaring", "kryobevaring"] 

termlist2_5e = ["plant bank", "seed bank", "genebank", "germplasm bank", 
                "cryobank","ex-situ", "cryopreserv", 
                
                "frøhvelv", "frøkvelv", "plantebank", "frøbank", "genbank", "genbevaring", "genressurssenter", "kimplasmabank", "kimplasmabevaring",
                "kryopreserv"
                ]

phrasedefault2_5d = r'(?:{})'.format('|'.join(termlist2_5d))
phrasedefault2_5e = r'(?:{})'.format('|'.join(termlist2_5e))
```


```python
#Search 1
Data.loc[(
   (Data['result_title'].str.contains(phrasedefault2_5c, na=False, case=False)) 
    & (
        (Data['result_title'].str.contains(phrasedefault2_5d, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault2_5e, na=False, case=False))
      )
    ),"tempsdg02_05"] = "SDG02_05"

print("Number of results = ", len(Data[(Data.tempsdg02_05 == "SDG02_05")])) 
```


```python
#Results
test=Data.loc[(Data.tempsdg02_05 == "SDG02_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4 & 5
```
TS=
(
  (
    ("genetic resource$" OR "agrobiodiversity"
    OR "plant bank$" OR "seed bank$" OR "gene bank$" OR "genebank$" OR "germplasm bank$"
    OR "cryobank$" OR "ex situ" OR "cryopreserv*" OR "germplasm"
    OR "seed commons"
    OR "bioprospecting"
    OR (("traditional" OR "indigenous" OR "autochthonous") NEAR/3 ("knowledge"))
    )
    NEAR/15
        ("governance" OR "justice" OR "ownership"
        OR "biopiracy" OR "inequitable" OR "inequity"
        OR "material transfer agreement$" OR "informed consent"
        OR "sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$"
        )
  )    
  AND
      ("food"
      OR "agricultur*" OR "domestic*" OR "farming" OR "farm$" OR "farmer$" OR "cultivar$" OR "permaculture"
      OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$"
      OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
      OR "aquaculture"
      OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
      OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
      OR "landrace$" OR "wild relative$"
      OR
        (
          ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
          NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
        )
      )                 
)   

TS =
(
    ("genetic resource$" OR "agrobiodiversity"
    OR "bioprospecting"
    OR (("traditional" OR "indigenous" OR "autochthonous") NEAR/3 ("knowledge" OR "right$"))
    )
    AND
        ("food"
        OR "agricultur*" OR "domestic*" OR "farming" OR "farm$" OR "farmer$" OR "cultiva*" OR "permaculture"
        OR "cropping system$" OR "orchard$" OR "arable land$" OR "pasture$"
        OR "agroforest*" OR "agro forest*" OR "silvopastur*" OR "silvopastoral*"
        OR "aquaculture"
        OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses"
        OR "livestock" OR "fish" OR "cattle" OR "sheep" OR "poultry" OR "pig$" OR "goat$" OR "chicken$" OR "buffalo*" OR "duck$"
        OR "landrace$" OR "wild relative$"
        OR
          (
            ("local*" OR "traditional" OR "heirloom" OR "wild" OR "indigenous" OR "autochthonous")
            NEAR/3 ("breed$" OR "variet*" OR "cultivar$")
          )
        )
    AND
        ("Convention on biological diversity" OR "CBD"
        OR "Nagoya Protocol"
        OR "International Seed Treaty"
        OR "biopiracy"
        OR "Global Plan of Action for Animal Genetic Resources"
        OR "Plant Genetic Resources for Food and Agriculture" OR "PGRFA"
        )
)
```


```python
#Termlists
termlist2_5f = ["genetic resource", "agrobiodiversity",
                "plant bank", "seed bank", "genebank", "germplasm bank", "cryobank",
                "ex-situ", "cryopreserv", 
                "seed commons",
                "bioprospect", 
                "traditional knowledge", "local knowledge", "indigenous knowledge","autochthonous knowledge", 
                
                "genetiske ressurs", "genressurs", 
                "frøhvelv", "frøkvelv","plantebank", "frøbank", "genbank", "genbevaring", "kimplasmabevaring", "kimplasmabank", "kimplasmaressurs",
                "kryopreserv",
                "frøallmenning",
                "bioprospekt",
                "tradisjonelle kunnskap", "tradisjonell kunnskap", "urfolkskunnskap", "urfolksperspektiv"
                ]
              
termlist2_5g = ["governance", "justice", "ownership",
                "biopira", "inequit", 
                "material transfer", "consent",
                "sharing", "equitab", "equal", "fair", "access", "right",
                "Convention on biological diversity", "CBD", 
                "Nagoya", 

                "myndig", "styring", "ledelse", "leiing", "rettferd", "eierskap", "eigarskap",
                "avtale",
                "deling", "deler", "tilgang", "rett",
                "Konvensjonen om biologisk mangfold"
                ] 

termlist2_5h = ["International Seed Treaty", 
                "Global Plan of Action for Animal Genetic Resources", "Plant Genetic Resources for Food and Agriculture", "PGRFA",
                "Den internasjonale plantetraktaten"
                ]

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

```
TS =
(
      ("Agriculture Orientation Index for Government Expenditure$"
      OR
        (
          (
            ("government" OR "public")
            NEAR/3 ("expenditure" OR "invest*" OR "financ*" OR "spending")
          )
        OR "ODA" OR "cooperation fund$" OR "development spending"
        OR
          (
            ("international" OR "development" OR "foreign")
            NEAR/3
                ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
                OR "aid" OR "assistance" OR "fund$" OR "funding" OR "financing" OR "finance" OR "grant$" OR "investment$" OR "financial support" OR "financial resources"
                )
          )
        )
        AND
            ("rural infrastructure"
            OR "agronom*" OR "agroecolog*" OR "agro ecolog*" OR "agricultural sector"
            OR "plant bank$" OR "seed bank$" OR "gene bank$" OR "genebank$" OR "germplasm bank$" OR "cryobank$"
            OR
              (
                ("infrastructure" OR "technolog*" OR "biotech*" OR "research" OR "science$" OR "innovation" OR "R&D")
                NEAR/3 ("agricultur*" OR "farm*" OR "irrigation" OR "agri food" OR "agrifood")
              )                  
            )
      )
      AND ****LMICs****
)
```


```python
#Termlists
termlist2_aa = ["Agriculture Orientation Index for Government Expenditure"]

termlist2_ab = ["government expenditure", "government spending", "public expenditure", "public spending",
                "investment", "financing", "fund", "grant", "financial resource",
                "ODA", "cooperation fund", "co-operation fund", "development spending",
                "international cooperation", "international co-operation", "international collaboration", "international network", "international partnership", "international aid", "international assistance",
                "development cooperation", "development co-operation", "development collaboration", "development network", "development partnership", "development aid", "development assistance",
                "foreign cooperation", "foreign co-operation", "foreign collaboration", "foreign network", "foreign partnership", "foreign aid", "foreign assistance",

                "statsbudsjett", "statsstøtte", "offentlig støtte", 
                "finansiel", "midlar", "økonomiske ressurs",
                "samarbeidsfond", "utviklingsstøtte", "utviklingsstønad", "bistand", "utviklingshjelp", "u-hjelp",
                "utviklingssamarbeid", "internasjonalt samarbeid", "internasjonale samarbeid"
                ]

termlist2_ac = ["rural infrastructure", "agronom", "agroecolog", "agricultural sector",
                "plant bank", "seed bank", "gene bank", "genebank", "germplasm bank", "cryobank",
                "agricultur", "farm", "irrigat", "agrifood", "agri food", "agri-food",

                "frøhvelv", "frøkvelv", "plantebank", "frøbank", "genbank", "genbevaring", "genressurssenter", "kimplasmabank", "kimplasmabevaring",
                "jordbruk", "landbruk", "gård", "gard", "småbruk", "familiebruk", "matprodusent", "matproduksjon"
                ]

phrasedefault2_aa = r'(?:{})'.format('|'.join(termlist2_aa))
phrasedefault2_ab = r'(?:{})'.format('|'.join(termlist2_ab))
phrasedefault2_ac = r'(?:{})'.format('|'.join(termlist2_ac))
```


```python
#Search - in LMICs
Data.loc[(
    (
      (Data['result_title'].str.contains(phrasedefault2_aa, na=False, case=False)) 
      |
        (
            (Data['result_title'].str.contains(phrasedefault2_ab, na=False, case=False)) 
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
test.iloc[0:5, ]
```

### SDG 2.b

*2.b Correct and prevent trade restrictions and distortions in world agricultural markets, including through the parallel elimination of all forms of agricultural export subsidies and all export measures with equivalent effect, in accordance with the mandate of the Doha Development Round.*

*Korrigere og hindre handelsrestriksjoner og vridninger på verdens landbruksmarkeder, blant annet gjennom en parallell avvikling av alle former for eksportsubsidier på landbruksvarer og alle eksporttiltak med tilsvarende effekt, i samsvar med mandatet for Doha-runden*

```
TS=
(
  ("export subsid*" OR "export credit$" OR "export financ*" OR "export competition" OR "export support$")
  AND ("agricultur*" OR "agrifood" OR "food")
)

TS=
(
  ("distort*" OR "price-fixing" OR "dumping"
  OR "trade restrict*" OR "Doha" OR "food aid"
  OR "state support*" OR "state financial support"
  OR "WTO dispute$"
  )
  NEAR/15
      (
        ("trade" OR "trading" OR "market$" OR "export$")
        NEAR/5 ("agricultur*" OR "agrifood" OR "food" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses")
      )
)

```


```python
#Termlists
termlist2_ba = ["export subsid","export credit","export financ","export competition","export support",
                "eksportsubsidi", "eksporttiltak", "eksportrestriksjon", "markeds-forstyrrende subsidi"
                ]

termlist2_bb = ["food", "agricultur", 
                "crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", 
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matprod", "gård", "landbruk", "jordbruk",
                "fiskeoppdrett", "lakseoppdrett",
                "grønnsak", "grønsak", "frukt", "fisk", "laks", "sau", "storfe", "svin", "fjærkre", "rein"
                ]

termlist2_bc = ["distort","price-fixing","dumping","trade restrict","Doha","food aid",
                "state support","state financial support",
                "WTO dispute",

                "vridning", "handelsrestriksjon", "matbistand",
                "verdens handelsorganisasjon", "verdas handelsorganisasjon", "handelsreform"
                ]

termlist2_bd = ["trade", "trading", "market", "export",         
                "handel", "marked", "marknad", "eksport"
                ]

phrasedefault2_ba = r'(?:{})'.format('|'.join(termlist2_ba))
phrasedefault2_bb = r'(?:{})'.format('|'.join(termlist2_bb))
phrasedefault2_bc = r'(?:{})'.format('|'.join(termlist2_bc))
phrasedefault2_bd = r'(?:{})'.format('|'.join(termlist2_bd))

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
test.iloc[0:5, ]
```

### SDG 2.c

*2.c Adopt measures to ensure the proper functioning of food commodity markets and their derivatives and facilitate timely access to market information, including on food reserves, in order to help limit extreme food price volatility.*

*Vedta tiltak for å sikre at råvare- og derivatmarkedene for matvarer er velfungerende og legge til rette for rask tilgang til markedsinformasjon, blant annet om matreserver, for å begrense ekstreme svingninger i matvareprisene*

```
TS=
(
    ("volatil*" OR "instability" OR "unstable" OR "anomalies" OR "price shock$" OR "price spike$" OR "inflation"
    OR "stability" OR "stable" OR "functioning"
    OR (("stabiliz*" OR "stabilis*") NEAR/5 ("price$" OR "market$"))
    )
    NEAR/15
        (
          ("price$" OR "market$")
          NEAR/5
            ("agricultur*" OR "agrifood" OR "food" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock")
        )
)
OR 
TS=
(
  ("price$"
  NEAR/3
    ("agricultur*" OR "agrifood" OR "food" OR "crop$" OR "grain$" OR "vegetable$" OR "fruit$" OR "cereal$" OR "rice" OR "wheat" OR "maize" OR "pulses" OR "livestock")
  ) 
  AND ("food market$" OR "agrifood market$" OR "agricultural market$" OR "commodity market$" OR "market information" OR "grain market$" OR "rice market$" OR "wheat market$")
)
```


```python
#Termlists
termlist2_ca = ["food", "agricultur", 
                " crop", "grain", "vegetable", "fruit", "cereal", " rice", "wheat", "maize", "pulses", 
                "livestock", "fish", "salmon", "cattle", "sheep", "poultry", "pigs", "goats", "chicken", "buffalo", "ducks", "reindeer",
                
                "matprod", "gård", "gard", "landbruk", "jordbruk",
                "fiskeoppdrett", "lakseoppdrett",
                "grønnsak", "grønsak", "frukt", "fisk", "laks", "sau", "storfe", "svine", "fjærkre", "rein"
                ]
                #"food" will find agrifood etc.
                #I've added a space before "crop" and "rice" to prevent "macro" and "price"
                #using "svine"(NO) here instead of svin, because we expect it to talk about svineprodukt, but also because it only adds 1 noisy result

termlist2_cb = ["price", "market", "trade", "trading",
                "pris", "kostnad", "marked", "marknad", "verdenshandel", "verdshandel", "internasjonal handel", "internasjonale handel"
                ]

termlist2_cc = ["volatil","anomalies","price shock","price spike","inflation","stabil","stable","function",
                
                "sving", "forutsig", "forutsei", "prishopp","prissjokk","inflasjon","funksjon"
                ]
                #"stabil" will find stabilis/ze, stability, instability, and the Norwegian term for stable/unstable (stabil, NO). 
                #"Volatil" will find the Norwegian word too.

termlist2_cd = ["price", 
                "pris", "kostnad"
                ]

termlist2_ce = ["market", "marknad", "trading", "trading", 
                "marked", "verdenshandel", "verdshandel", "internasjonal handel", "internasjonale handel"
                ]

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

```
TS=
("SDG 2" OR "SDGs 2" OR "SDG2" OR "sustainable development goal$ 2"
OR ("sustainable development goal$" AND "goal 2")
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 2")
    AND ("zero hunger")
  )
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 2")
    NEAR/15 ("hunger" OR "food")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  OR "Millennium Development Goal 2"
  )
```


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
      |
      (
        (Data['result_title'].str.contains(phrasedefault_sdg_b, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault_sdg_c, na=False, case=False))
      )
      |
      (
         (Data['result_title'].str.contains(phrasespecific_sdg_d, na=False, case=False))
         & (Data['result_title'].str.contains(phrasedefault_sdg_e, na=False, case=False))
      )
    ),"tempmentionsdg02"] = "SDG02"

print("Number of results = ", len(Data[(Data.tempmentionsdg02 == "SDG02")])) 
```


```python
test=Data.loc[(Data.tempmentionsdg02 == "SDG02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

## SDG 3

Webpages about SDG targets from the UN Association of Norway were used to help with Norwegian terms (https://www.fn.no/om-fn/fns-baerekraftsmaal/god-helse-og-livskvalitet).

Have also used "Realfagstermer", a controlled vocabulary for scientific terms from the University of Oslo and University of Bergen - https://app.uio.no/ub/emnesok/realfagstermer/search

### SDG 3.1

*By 2030, reduce the global maternal mortality ratio to less than 70 per 100,000 live births.*

*Innen 2030 redusere mødredødeligheten i verden til under 70 per 100 000 levendefødte*


```
TS=
(
  (   
    ("pregnan*" OR "post partum" OR "postpartum" OR "peripartum" OR "obstetric$"
    OR "childbirth" OR "child-birth" OR "birth" OR "births"
    OR "premature deliver*" OR "preterm deliver*" OR "preterm labor" OR "preterm labour"
    OR "maternal" OR "mothers"
    )
    NEAR/15
        ("mortality" OR "death$")
  )
  NOT (("pigs" OR "cows" OR "sheep" OR "cattle" OR "poultry") NOT ("human" OR "model"))    
)
```

Because this is a title search, it is less important with the NOT search (it does not seem to cause as much noise). It may be more important for use on other research sets which have large amounts of agricultural research. 


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

Phrase 1 & Phrase 2
```
TS=
(
  (   
    ("child*" OR "infant$" OR "toddler$" OR "under-five$"
    OR "baby" OR "babies" OR "newborn$" OR "neonatal" OR "neonate$"
    OR "perinatal" OR "prenatal" OR "antenatal"
    )
    NEAR/15
        ("mortality" OR "death$" OR "stillbirth$" OR "still-birth$")
  )
  NOT (("pigs" OR "cows" OR "sheep" OR "cattle" OR "poultry") NOT ("human" OR "model"))    
)

TS=
(
  (   
    ("child*" OR "infant$" OR "toddler$" OR "under-five$"
    OR "baby" OR "babies" OR "newborn$" OR "neonatal" OR "neonate$"
    OR "perinatal" OR "prenatal" OR "antenatal"
    )
    NEAR/15
      ("surviv*")
  )
  NOT (("pigs" OR "porcine" OR "cows" OR "sheep" OR "cattle" OR "poultry" OR "newborn cell") NOT ("human" OR "model"))   
)
```


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
              #it would be strange not to include the words "baby", "newborn" etc. together with premature.

termlist3_2b = ["mortality","death","stillbirth","still-birth", "surviv",
                "mortalitet", "død", "overleve"
                ]

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
```
TS =
(
  (
    ("communicable disease$" OR "communicable illness*")
    NEAR/15
        ("prevent$" OR "preventing" OR "prevention" OR "prevented" OR "combat*" OR "fight*" OR "tackl*" OR "reduc*" OR "alleviat*" OR "mitigat*"
        OR "eradicat*" OR "eliminat*" OR "end" OR "ended" OR "ending"
        OR "treat" OR "cure" OR "cured" OR "vaccinate" OR "control"
        OR "epidemic$" OR "pandemic$" OR "outbreak$" OR "spread" OR "transmission" OR "occurrence" OR "incidence" OR "prevalence" OR "risk$" OR "rate$"
        OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "treatment$" OR "intervention$" OR "therap*"
        )
  )
  NOT ("non communicable" NOT ("infectious disease$" OR "tropical disease$" OR "non communicable and communicable" OR "communicable and non communicable"))
)
```


```python
#Termlists
termlist3_3a = ["communicable disease", "communicable illness",
                "overførbar sykdom", "overførbare sykdommer", "smittsom sykdom", "smittsomme sykdommer", "smittsam sjukdom", "smittsame sjukdommar"] 
termlist3_3b = ["prevent","combat","fight","tackl","reduc","alleviat","mitigat",
                "eradicat","eliminat","end","ended","ending",
                "treat","cure","vaccin","control",
                "epidemic","pandemic","outbreak","spread","transmission","occurrence","incidence","prevalence","risk","rate",
                "medicine","drug","intervention","therap"
                
                "hindr", "forebygg", "førebygg", "kjemp", "takl", "reduser", "reduksjon", "lett", "mink",
                "utrydd", "eliminer", "stopp", "stogg",
                "behandl", "kurer", "vaksine", "kontroll"
                "epidemi", "pandemi", "utbrudd", "utbrot", "spre", "smitte", "overføring", "forekom", "førekom", "tilfelle", "utbre", "risik",
                "medisin", "legemid", "intervensjon", "terap"]
termlist3_3c = ["non-communicable disease", "non-communicable illness", "noncommunicable disease", "noncommunicable illness", 
                "ikke smittsom sykdom", "ikke-smittsom sykdom", "ikke-smittsomme sykdom", "ikkje-smittsam sjukdom", "ikkje smittsame sjukdom" ]
termlist3_3d = ["infectious disease", "tropical illness",
                "non communicable and communicable","communicable and non communicable","non-communicable and communicable","communicable and non-communicable",
                "noncommunicable and communicable","communicable and noncommunicable",
                "overførbar", "tropisk sykdom", "tropiske sykdom", "tropesykdom", "tropisk sjukdom", "tropiske sjukdom", "tropesjukdom", 
                "ikke-smittsom og smittsom", "ikke-smittsomme og smittsomme", "smittsom og ikke-smittsom", "smittsomme og ikke-smittsomme",
                "ikkje-smittsam og smittsam", "ikkje-smittsame og smittsame", "smittsam og ikkje-smittsam", "smittsame og ikkje-smittsame"]            

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

#### Phrase 2 & 3


```
Phrase 2
TS =
(
  (
    (
      ("water borne" OR "waterborne" OR "water-borne" OR "water-related" OR "diarrhoea*" OR "diarrhea*"
      OR "contagious" OR "transmissible" OR "infectious"
      )
      NEAR/5
          ("disease$" OR "infection$" OR "epidemic$" OR "illness*")
    )
    OR "hepatitis"
    OR "acquired immune deficiency syndrome" OR "acquired immuno-deficiency syndrome"  OR "acquired immunodeficiency syndrome" OR "Human Immunodeficiency Virus" OR "HIV" OR "prevent aids"
    OR "tuberculosis"
    OR "malaria"
    OR "cholera"
    OR "meningitis"
    OR "influenza" OR "avian influenza" OR "H5N1"
    OR "rubella"
    OR "diphtheria"
    OR "japanese encephalitis"
    OR "measles"
    OR "mumps"
    OR "tetanus"
    OR "pertussis"
    OR "polio*"
    OR "yellow fever"
    OR "sexually transmitted disease$" OR "sexually transmitted infection$"
    OR "syphilis"
    OR "lower respiratory infection$"
    OR "coronavirus" OR "covid" OR "covid19" OR "middle east respiratory syndrome" OR "MERS" OR "severe acute respiratory syndrome" OR "SARS"
    OR "crimean-congo haemorrhagic fever" OR "viral haemorrhagic fever$"
    OR "ebola"
    OR "plague"
    OR "rift valley fever"
    OR "zika virus"

    OR "amebiasis"
    OR "cryptosporidiosis" OR "cryptosporidium infection$"
    OR "giardiasis" OR "giardia infection$"
    OR "shigellosis"
    OR "cronobacter infection$"
    OR "acanthamoeba"
    OR "balamuthia"
    OR "naegleria"
    OR "sappinia"
    OR "typhoid"

    OR "neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthias*" OR "hookworm$" OR "roundworm$" OR "whipworm$" OR "Ascaris lumbricoides" OR "Trichuris trichiura" OR "Necator americanus" OR "Ancylostoma duodenale"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
  )
  NEAR/5
      ("prevent$" OR "preventing" OR "prevention" OR "prevented" OR "combat*" OR "fight*" OR "tackl*" OR "reduc*" OR "alleviat*" OR "mitigat*"
      OR "eradicat*" OR "eliminat*" OR "end" OR "ended" OR "ending"
      OR "treat" OR "cure" OR "cured" OR "vaccinate" OR "control"
      )
)

Phrase 3
TS =
(
  (
    (
      ("water borne" OR "waterborne" OR "water-borne" OR "water-related" OR "diarrhoea*" OR "diarrhea*"
      OR "contagious" OR "transmissible" OR "infectious"
      )
      NEAR/5
          ("disease$" OR "infection$" OR "epidemic$" OR "illness*")
    )
    OR "hepatitis"
    OR "acquired immune deficiency syndrome" OR "acquired immuno-deficiency syndrome"  OR "acquired immunodeficiency syndrome" OR "Human Immunodeficiency Virus" OR "HIV" OR "prevent aids"
    OR "tuberculosis"
    OR "malaria"
    OR "cholera"
    OR "meningitis"
    OR "influenza" OR "avian influenza" OR "H5N1"
    OR "rubella"
    OR "diphtheria"
    OR "japanese encephalitis"
    OR "measles"
    OR "mumps"
    OR "tetanus"
    OR "pertussis"
    OR "polio*"
    OR "yellow fever"
    OR "sexually transmitted disease$" OR "sexually transmitted infection$"
    OR "syphilis"
    OR "lower respiratory infection$"
    OR "coronavirus" OR "covid" OR "covid19" OR "middle east respiratory syndrome" OR "MERS" OR "severe acute respiratory syndrome" OR "SARS"
    OR "crimean-congo haemorrhagic fever" OR "viral haemorrhagic fever$"
    OR "ebola"
    OR "plague"
    OR "rift valley fever"
    OR "zika virus"

    OR "amebiasis"
    OR "cryptosporidiosis" OR "cryptosporidium infection$"
    OR "giardiasis" OR "giardia infection$"
    OR "shigellosis"
    OR "cronobacter infection$"
    OR "acanthamoeba"
    OR "balamuthia"
    OR "naegleria"
    OR "sappinia"
    OR "typhoid"

    OR "neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthias*" OR "hookworm$" OR "roundworm$" OR "whipworm$" OR "Ascaris lumbricoides" OR "Trichuris trichiura" OR "Necator americanus" OR "Ancylostoma duodenale"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
  )
  AND
      ("epidemic$" OR "pandemic$" OR "outbreak$" OR "spread" OR "transmission" OR "occurrence" OR "incidence" OR "prevalence" OR "risk$" OR "rate$"
      OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "cure" OR "treatment$" OR "drug$" OR "intervention$" OR "therap*"
      OR "antimalarial$" OR "antiviral$" OR "antibiotic$" OR "antiparasitic$" OR "antihelminthic$" OR "antihelmintic$"
      )
)
```



```python
#Termlists 
termlist3_3e = ["water borne", "waterborne", "water-borne", "water-related", "diorrhea", "diarrhea", "contagious", "transmissible", "infectious",
                "vannbår", "vassbår", "vassbor", "vannrelatert", "diare", "smittsom", "smittsam", "smitte", "overførbar"]
termlist3_3f = ["disease", "infection", "epidemic", "illness", 
                "sykdom", "sjukdom", "infeksjon", "epidemi"]
termlist3_3g = ["hepatitis", "acquired immune deficiency syndrome", "acquired immuno-deficiency syndrome", "acquired immunodeficiency syndrome", "Human Immunodeficiency Virus", "prevent aids",
                "tuberculosis", "malaria", "cholera", "meningitis", "influenza", "avian influenza", "h5n1", "rubella", "diphteria", "japanese encephalitis", "measles", "mumps", "tetanus",
                "pertussis", "polio", "yellow fever", "sexually transmitted disease", "sexually transmitted infection", "syphilis", "lower respiratory infection",
                "coronavirus", "covid", "covid19", "middle east respiratory syndrome", "severe acute respiratory syndrome",
                "crimean-congo haemorrhagic fever", "viral haemorrhagic fever", "ebola", "plague", "rift valley fever", "zika virus",
                "amebiasis", "cryptosporidiosis", "cryptosporidium infection", "giardiasis", "giardia infection", "shigellosis", "cronobacter infection"
                "acanthamoeba", "balamuthia", "naegleria", "sappinia", "typhoid", 
                "neglected tropical disease", "buruli ulcer", "chagas", "dengue", "chikungunya", "dracunculiasis", "guinea-worm disease", "echinococcosis", "foodborne trematodiases",
                "human african trypanosomiasis", "sleeping sickness", "leishmaniasis", "leprosy", "lymphatic filariasis", "mycetom", "chromoblastomycosis", "deep mycoses",
                "onchocerciasis", "river blindness", "rabies", "scabies", "schistosomiasis", "soil-transmitted helminthiasis", "hookworm", "roundworm", "whipworm", "ascaris lumbricoides",
                "trichuris trichiura", "necator americanus", "ancylostoma duodenale", "snakebite envenoming", "taeniasis", "cysticercosis", "trachoma", "yaws",
                "trichuris", "necator", "ancylostoma",
                
                "hepatitt", "ervervet immunsvikt syndrom-virus", "humant immunsviktvirus", "hindre aids",
                "tuberkulose", "kolera", "meningitt", "influensa", "røde hunder", "difteri", "japansk encefalitt", "meslinger", "kusma", "stivkrampe",
                "kikhoste", "gulfeber", "seksuelt overførbar", "syfilis", "luftveisinfeksjon", "koronavirus", 
                "krimfeber", "rift valley-feber", "zikavirus",
                "amøbiasis", "kryptosporidiose", "giardiainfeksjon", "shigellose", "enterobakterieinfeksjon", "tyfoidfeber",         
                "neglisjert tropesykdom", "neglisjerte tropesjukdom", "neglisjert tropesjukdom", "negliserte tropesjukdom", "burulisår", "ekinokkokose", "trematodeinfeksjon",
                "afrikansk trypanosomiasis", "lepra", "lymfatisk filariasis", "mykose", "kromomykose",
                "onkocerkose", "skabb", "helmintiasis", "jordoverført helminthiasis", "hakeorm", "rundorm", "guineaorm", 
                "taeniainfeksjon", "cysticerkose", "trakom", "frambøsi"
                ]
termlist3_3h = ["pest"]                
termlist3_3i = ["HIV", "AIDS", "MERS", "SARS"]
termlist3_3j = ["prevent", "combat", "fight", "tackl", "reduc", "alleviat", "mitigat", "eradicat", "eliminat", "treat", "cure", "vaccinate", "control",
                "hindr", "forebygg", "førebygg", "nedkjemp", "takl", "overvinn", "lette", "utrydde", "elimin", "stopp", "stogg", "behandl", "kurer", "vaksiner", "kontroll"]
termlist3_3k = ["epidemi", "pandemi", "outbreak", "spread", "transmission", "occurrence", "incidence", "prevalence", "risk", "rate",
                "medicine", "drug", "treatment", "drug", "intervention", "therap", 
                "antimalaria", "antiviral", "antibioti", "antiparasitic", "antihelminthic", 

                "utbrudd", "spredning", "spreiing", "smitte", "overføring", "forekomst", "førekomst", "hendelse", "hending", "utbredelse", "utbreiing", "risik",
                "medisin", "legemiddel", "medikament", "intervensjon", "terap", "antihelminti"
               ]

phrasedefault3_3e = r'(?:{})'.format('|'.join(termlist3_3e))
phrasedefault3_3f = r'(?:{})'.format('|'.join(termlist3_3f))
phrasedefault3_3g = r'(?:{})'.format('|'.join(termlist3_3g))
phrasespecific3_3h = r'(?:{})\b'.format('|'.join(termlist3_3h))
phrasedefault3_3i = r'(?:{})'.format('|'.join(termlist3_3i))
phrasedefault3_3j = r'(?:{})'.format('|'.join(termlist3_3j))
phrasedefault3_3k = r'(?:{})'.format('|'.join(termlist3_3k))

```


```python
#Search 
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault3_3e, na=False, case=False))&
            (Data['result_title'].str.contains(phrasedefault3_3f, na=False, case=False))
        )
    |
     (
      (Data['result_title'].str.contains(phrasedefault3_3g, na=False, case=False))
      |
      (Data['result_title'].str.contains(phrasespecific3_3h, na=False, case=False))
      |
      (Data['result_title'].str.contains(phrasedefault3_3i, na=False, case=True))
     )
    )
    &
     (
         (Data['result_title'].str.contains(phrasedefault3_3j, na=False, case=False))|
         (Data['result_title'].str.contains(phrasedefault3_3k, na=False, case=False))
      
     )
    ),"tempsdg03_03"] = "SDG03_03"

print("Number of results = ", len(Data[(Data.tempsdg03_03 == "SDG03_03")])) 
```


```python
test=Data.loc[(Data.tempsdg03_03 == "SDG03_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 3.4

*By 2030, reduce by one third premature mortality from non-communicable diseases through prevention and treatment and promote mental health and well-being.*

*Innen 2030 redusere prematur dødelighet forårsaket av ikke-smittsomme sykdommer med en tredel gjennom forebygging og behandling, og fremme mental helse og livskvalitet*

#### Phrase 1

```
TS=
(
  (
    (
      ("non communicable" OR "noncommunicable" OR "non transmissible" OR "non infectious" OR "noninfectious")
      NEAR/5
          ("disease$" OR "illness*")
    )
    OR "cardiovascular disease$" OR "heart disease" OR "heart attack$" OR "stroke$"
    OR "diabetes"
    OR "chronic respiratory disease$" OR "asthma"  OR "emphysema" OR "chronic obstructive pulmonary disease$" OR "COPD" OR "chronic obstructive airway disease$" OR "chronic bronchitis"
    OR (("chronic") NEAR/3 ("lung" OR "pulmonary"))
    OR "cancer$" OR "*sarcoma" OR "sarcoma$" OR "*carcinoma" OR "carcinoma$" OR "*blastoma" OR "blastoma$" OR "myeloma$" OR "lymphoma$" OR "leukaemia" OR "leukemia" OR "mesothelioma$" OR "melanoma$"  
    OR (("malignant" OR "incurable") NEAR/3 ("neoplasm$" OR "tumour$" OR "tumor$"))
    OR "kidney disease$"
    OR "alzheimer*" OR "dementia"
    OR "cirrhosis"
  )
  NEAR/15
      ("mortality" OR "death$" OR "surviv*")
)
```



```python
#Termlists 
termlist3_4a = ["non communicable", "noncommunicable", "non-communicable", "non transmissible", "nontransmissible", "non-transmissible", 
                "non infectious", "noninfectious", "non-infectious",
                "ikke-smittsom", "ikkje-smittsam", "ikke smittsom", "ikkje smittsam"]
termlist3_4b = ["disease", "illness", 
                "sykdom", "sjukdom"]
termlist3_4c = ["cardiovascular disease", "heart disease", "heart attack", "stroke", "diabetes",
                "chronic respiratory disease", "asthma", "emphysema", "chronic obstructive pulmonary disease",
                "COPD", "chronic obstructive airway disease", "chronic bronchitis", 
                "cancer", "sarcoma", "carcinoma", "blastoma", "myeloma", "lymphoma", "leukaemia", "leukemia",
                "mesothelioma", "melanom", "kidney disease", "alzheimer", "dementia", "cirrhosis",
                
                "kardiovaskulær sykdom", "kardiovaskulære sykdom", "kardiovaskulær sjukdom", "kardiovaskulære sjukdom",
                "hjertesykdom", "hjartesjukdom", "hjerteinfarkt", "hjarteinfarkt", "hjerteanfall", "hjarteanfall", "hjerteattakk", "hjarteattakk", "slag",
                "kronisk luftvei", "astma", "emfysem", "kronisk obstruktiv lungesykdom", "kronisk obstruktiv lungesjukdom", "kols", "kronisk bronkitt",
                "kreft", "sarkom", "karsinom", "blastom", "lymfom", "leukemi",
                "mesoteliom", "nyresykdom", "nyresjukdom", "demens"]
termlist3_4d = ["chronic", 
                "kronisk"]
termlist3_4e = ["lung", "pulmonar"]    
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
        (
            ( 
              (Data['result_title'].str.contains(phrasedefault3_4a, na=False, case=False))&
              (Data['result_title'].str.contains(phrasedefault3_4b, na=False, case=False)) 
            )
            |
          (Data['result_title'].str.contains(phrasedefault3_4c, na=False, case=False))
            |
          (  
           (Data['result_title'].str.contains(phrasedefault3_4d, na=False, case=False))&
           (Data['result_title'].str.contains(phrasedefault3_4e, na=False, case=False))  
           ) 
            |
          (
              (Data['result_title'].str.contains(phrasedefault3_4f, na=False, case=False))&
              (Data['result_title'].str.contains(phrasedefault3_4g, na=False, case=False))
          )
        )
        &
     (Data['result_title'].str.contains(phrasedefault3_4h, na=False, case=False))
    )
    ),"tempsdg03_04"] = "SDG03_04"

print("Number of results = ", len(Data[(Data.tempsdg03_04 == "SDG03_04")]))

```

#### Phrase 2
```
TS=
(
  ("mental health disorder$" OR "mental illness*"
  OR "suicid*"
  OR "depression" OR "depressive disorder$"
  OR "bipolar affective disorder"
  OR "schizophrenia"
  OR "psychosis" OR "psychoses"
  )
  NEAR/15
      ("prevent*" OR "combat*" OR "fight*" OR "reduc*" OR "alleviat*" OR "eradicat*" OR "eliminat*" OR "tackl*"
      OR "treat" OR "cure" OR "cured"
      OR "epidemic$" OR "occurrence" OR "incidence" OR "prevalence" OR "risk$" OR "rate$"
      OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "cure" OR "treatment$" OR "drug$" OR "intervention$" OR "therap*"
      OR "outreach" OR "services" OR "support" OR "counseling" OR "counselling"
      )
)
  
```


```python
#Termlists
termlist3_4h = ["mental health disorder", "mental illness", "suicid", "depression", "depressive disorder",
                "bipolar affective disorder", "schizophrenia", "psychosis", "psychoses",
                
                "psykisk lidelse", "psykisk liding", "psykisk syk", "psykisk sjuk", "selvmord", "sjølmord", "sjølvmord", "depresjon", "depressiv lid",
                "bipolar lid", "schizofreni", "psykose"]
termlist3_4i = ["prevent", "combat", "fight", "reduc", "alleviat", "eradicat", "eliminat", "tackl", "treat", "cure",
                "epidemi", "occurrence", "incidence", "prevalence", "risk", "rate",
                "medicine", "vaccin", "drug", "treatment", "intervention", "therap",
                "outreach", "services", "support", "counseling", "counselling",
                
                "hindr", "forebygg", "førebygg", "kjemp", "reduser", "reduksjon", "utrydd", "eliminer", "takl", "behandl", "kurer", 
                "forekom", "førekom", "hendelse", "hending", "tilfelle", "utbre", "risik",
                "medisin", "vaksin", "legemid", "medikament", "behandling", "intervensjon", "terap",
                "støtte", "stønad", "tjeneste", "teneste", "rådgiv", "rådgjev"]       
                            
phrasedefault3_4h = r'(?:{})'.format('|'.join(termlist3_4h))
phrasedefault3_4i = r'(?:{})'.format('|'.join(termlist3_4i))
```


```python
#Search 3_4hi
Data.loc[(
        (Data['result_title'].str.contains(phrasedefault3_4h, na=False, case=False)) &
        (Data['result_title'].str.contains(phrasedefault3_4i, na=False, case= False)) 
    ),"tempsdg03_04"] = "SDG03_04"

print("Number of results = ", len(Data[(Data.tempsdg03_04 == "SDG03_04")])) 
```

#### Phrase 3

```
TS=
(
  ("mental health" OR "well being" OR "wellbeing")
  NEAR/15
      ("promot*" OR "strengthen*" OR "improv*" OR "enhanc*"
      OR (("reduc*" OR "decreas*") NEAR/5 "problem$")
      OR "medicine$" OR "vaccin*" OR "drug$" OR "cures" OR "cure" OR "treatment$" OR "drug$" OR "intervention$" OR "therap*"
      OR "outreach" OR "services" OR "support" OR "counseling" OR "counselling"
      )  
)
```



```python
#Termlists
termlist3_4j = ["mental health", "well being", "wellbeing", 
                "mental helse", "velvære", "god helse"]
termlist3_4k = ["promot", "strengthen", "improv", "enhanc", "medicine", "vaccin", "drug", "cure", "treatment", "intervention", 
                "therap", "outreach", "services", "support", "counselling", "counseling",

                "fremme", "fremje", "styrke", "bedre", "betre", "øke", "auke", "medisin", "vaksine", "medikament", "legemid", "kurer", "behandl", "intervensjon"
                "terap", "tjeneste", "teneste", "støtte", "stønad", "rådgi", "rådgje"]
termlist3_4l = ["reduc", "decreas", 
                "reduser", "mink"]
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
         (Data['result_title'].str.contains(phrasedefault3_4l, na=False, case=False))&
         (Data['result_title'].str.contains(phrasedefault3_4m, na=False, case=False))
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


```
TS=
(
  ("binge drinking" OR "binge drinker$" OR "alcoholism" OR "excessive drinking" OR "problematic drinking"
  OR "substance use" OR "illicit drug$" OR "people who inject drugs" OR "PWID"
  OR "opioid epidemic"
  OR
    (
      ("drug$" OR "narcotic$" OR "narcotic$" OR "substance"
      OR "alcohol"
      OR "amphetamine$" OR "methamphetamine$" OR "MDMA" OR "ecstasy"
      OR "cocaine"
      OR "inhalant$" OR "amyl nitrite"
      OR "marijuana" OR "cannabis"
      OR "opioid$" OR "opiate$" OR "heroin" OR "morphine"
      OR "phencyclidine" OR "LSD" OR "psilocybin" OR "dimethyltriptamine"
      OR "khat"
      OR "tobacco"
      )
      NEAR/15
          ("abuse" OR "misuse" OR "dependence" OR "addict*" OR "overdose$"
          OR
            (
              ("use" OR "uses" OR "usage" OR "consumption")
              NEAR/3 ("harmful" OR "problematic" OR "excessive" OR "disorder$")    
            )
          )
    )
  )
  NEAR/5
      ("prevent$" OR "preventing" OR "prevention" OR "prevented" OR "combat*" OR "tackl*" OR "fight* against"
      OR "reduc*" OR "decreas*" OR "minimi*" OR "limit" OR "limiting" OR "alleviat*" OR "mitigat*"
      OR "eradicat*" OR "eliminat*" OR "end" OR "ended" OR "ending" OR "stop" OR "stopped" OR "stopping"
      OR "treat" OR "cure" OR "cured" OR "control"
      )
)
OR
TS=
(
  ("binge drinking" OR "binge drinker$" OR "alcoholism" OR "excessive drinking" OR "problematic drinking"
  OR "substance use" OR "illicit drug$" OR "people who inject drugs" OR "PWID"
  OR "opioid epidemic"
  OR
    (
      ("drug$" OR "narcotic$" OR "narcotic$" OR "substance"
      OR "alcohol"
      OR "amphetamine$" OR "methamphetamine$" OR "MDMA" OR "ecstasy"
      OR "cocaine"
      OR "inhalant$" OR "amyl nitrite"
      OR "marijuana" OR "cannabis"
      OR "opioid$" OR "opiate$" OR "heroin" OR "morphine"
      OR "phencyclidine" OR "LSD" OR "psilocybin" OR "dimethyltriptamine"
      OR "khat"
      OR "tobacco"
      )
      NEAR/15
          ("abuse" OR "misuse" OR "dependence" OR "addict*" OR "overdose$"
          OR
            (
              ("use" OR "uses" OR "usage" OR "consumption")
              NEAR/3 ("harmful" OR "problematic" OR "excessive" OR "disorder$")    
            )
          )
    )
  )
  NEAR/15
      ("medicine$" OR "cures" OR "cure" OR "treatment$" OR "intervention$" OR "therapy" OR "therapies"
      OR "outreach" OR "services" OR "support" OR "rehabilitat*" OR "aftercare" OR "counseling" OR "counselling"
      )
)
```


```python
#Termlists
termlist3_5a = ["binge drinking", "binge drinker", "alcohol", "excessive drinking", "problematic drinking", 
                "substance use", "illicit drugs", "people who inject drugs", "PWID", "opiod epidemic",
                "alkohol", "periodedrank", "periodedrikk", "narkotikamisbruk", "stoffmisbruk", "opioidepidemi"]
termlist3_5atrunk = ["fyll"]              
termlist3_5b = ["drug", "narcotic", "substance", "alcohol", "amphetamine", "metamphetamine", "MDMA", "ecstacy", "cocaine", "inhalant", "amyl nitrate",
                "marijuana", "cannabis", "opioid", "opiat", "heroin", "morphine", "phencyclidine", "LSD", "psilocybin", "dimethyltriptamin", "khat", "tobacco",
                "rusmid", "narkotik", "stoff", "alkohol", "amfetamin", "metamfetamin", "kokain", "inhalasjon", "inhalering", "amylnitrat", 
                "marihuana", "hasj", "morfin", "fensyklidin", "tobakk"]
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
            (
              (Data['result_title'].str.contains(phrasedefault3_5a, na=False, case=False))
              |
              (Data['result_title'].str.contains(phrasespecific3_5atrunk, na=False, case=False))
            )  
            |
        (
          (Data['result_title'].str.contains(phrasedefault3_5b, na=False, case=False)) &
           (
              (Data['result_title'].str.contains(phrasedefault3_5c, na=False, case=False))|
              (
                  (Data['result_title'].str.contains(phrasedefault3_5d, na=False, case=False))&
                  (Data['result_title'].str.contains(phrasedefault3_5e, na=False, case=False))
              )
           )   
         )
        )
        &
     (
     (Data['result_title'].str.contains(phrasedefault3_5f, na=False, case=False))|
     (Data['result_title'].str.contains(phrasedefault3_5g, na=False, case=False))
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


```
TS =
(
  (
      ("traffic" OR "road" OR "roads" OR "roadway$" OR "street$" OR "roundabout$" OR "highway$" OR "motorway$"
      OR "cycling lane$" OR "cycle path$" OR "bicycle lane$" OR "walkway$" OR "walking path$" OR "sidewalk$" OR "pavement$"
      OR "bicycle$" OR "motorcycle$" OR "motorbike$" OR "automobile$" OR "buses" OR "bus" OR "lorry" OR "lorries" OR "truck$" OR "HGV$" OR "SUV$"
      OR "pedestrian$" OR "cyclist$"
      OR "driving fatalities"
      OR (("vehicle$" OR "driver$" OR "driving" OR "car" OR "cars") NEAR/15 ("accident$" OR "crash*" OR "collision$" OR "traffic" OR "RTI" OR "RTIs"))
      )
      AND
          ("mortality" OR "death$" OR "fatalities" OR "fatal" OR "deadly"
          OR "morbidity" OR "injury" OR "injuries" OR "road trauma$" OR "RTI" OR "RTIs"
          )
  )
  NOT ("air traffic" OR "boat traffic")
)

```


```python
#Termlists
termlist3_6a = ["traffic", "roadway", "street", "roundabout", "highway", "motorway", "cycling lane", "cycle path", "bicycle lane", 
                "walkway", "walking path", "sidewalk", "pavement", "bicycles", "motorcycles", "motorbike", "automobile", "lorry", "lorries",
                "truck", "pedestrian", "cyclist", "driving fatalities",
                
                "trafikk", "rundkjøring", "rundkøyring", "motorvei", "motorveg", "sykkelsti", "sykkelve", 
                "gangve", "fortau", "sykkel", "sykler", "syklar", "motorsykkel", "motorsykler", "motorsyklar", "buss", "fotgjenger", "syklist", "trafikkdød", "trafikkulykke", 
                "trafikkulukke", "bilulykke", "bilulukke"]
termlist3_6btrunk = ["bus", "buses", "HGV", "HGVs", "SUV", "SUVs", "road", "roads", 
                     "vei", "veier", "veg", "veger", "vegar", "gående", "gåande"]
termlist3_6b = ["vehicle", "driver", "driving", "car", 
                "kjøretøy", "køyretøy", "fører", "førar", "sjåfør", "kjøring", "køyring", "bil"] 
termlist3_6c = ["accident", "crash", "collision", "traffic", 
                "ulykke", "ulukke", "kræsj", "kollisjon", "trafikk"]
termlist3_6d = ["mortal", "death", "fatal", "deadly", "morbidity", "injury", "injuries", "injured", "road trauma",
                "dødelig", "dødeleg", "døyeleg", "død", "skade", "skadd"] 
termlist3_6e = ["air traffic", "boat traffic"]
  
phrasedefault3_6a = r'(?:{})'.format('|'.join(termlist3_6a))
phrasespecific3_6btrunk = r'\b(?:{})\b'.format('|'.join(termlist3_6btrunk))
phrasedefault3_6b = r'(?:{})'.format('|'.join(termlist3_6b))
phrasedefault3_6c = r'(?:{})'.format('|'.join(termlist3_6c))
phrasedefault3_6d = r'(?:{})'.format('|'.join(termlist3_6d))
phrasedefault3_6e = r'(?:{})'.format('|'.join(termlist3_6e))
```


```python
#Search 3_6
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault3_6a, na=False, case=False))
            |(Data['result_title'].str.contains(phrasespecific3_6btrunk, na=False, case=False))
        )
        |
        (
            (Data['result_title'].str.contains(phrasedefault3_6b, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault3_6c, na=False, case=False))
        )
    )
    & (Data['result_title'].str.contains(phrasedefault3_6d, na=False, case=False))     
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

```
TS =
(
  ("reproductive health" OR "sexual health" OR "reproductive healthcare" OR "sexual healthcare"
  OR "family planning" OR "planned pregnanc*" OR "contracept*" OR "abortion$"
  OR (("reproduct*" OR "sex*" OR "STI") NEAR/5 ("education" OR "inform*" OR "health literacy"))
  )
  NEAR/15
      ("health equity" OR "equity in health*" OR "health for all"
      OR "access*" OR "right$" OR "coverage"
      OR "afford" OR "affordab*" OR "low cost" OR "free of charge" OR "free service$" OR "subsidi*"
      OR "barrier$" OR "obstacle$" OR "impediment$" OR "unaffordab*" OR "expensive"
      )
)       
```


```python
#Termlists
termlist3_7a = ["reproductive health", "sexual health", "family planning", "planned pregnanc", "contracept", "abortion",
                "reproduksjonshelse", "reproduktiv helse", "seksuell helse", "familieplanlegging", "planlagt graviditet", "prevensjon", "abort"]
termlist3_7b = ["reproduct", "sex", 
                "reproduk"]
termlist3_7c = ["education", "inform", "health literacy", 
                "utdann", "opplær", "opplys", "kompetanse"]
termlist3_7d = ["health equity", "equality in health", "health for all", "access", "right", "coverage", "afford", "low cost", "free of charge", "free service", "subsidi",
                "barrier", "obstacle", "impediment", "unaffordab", "expensive",
                "rettferdig helse", "tilgang", "adgang", "åtgang", "rett", "dekning", "rimelig", "rimeleg", "billig", "billeg", "gratis", "hindr", "hinder", "dyr", "kostbar"]

phrasedefault3_7a = r'(?:{})'.format('|'.join(termlist3_7a))
phrasedefault3_7b = r'(?:{})'.format('|'.join(termlist3_7b))
phrasedefault3_7c = r'(?:{})'.format('|'.join(termlist3_7c))
phrasedefault3_7d = r'(?:{})'.format('|'.join(termlist3_7d))
```


```python
#Search 1
Data.loc[(
            (
              (Data['result_title'].str.contains(phrasedefault3_7a, na=False, case=False))|
               (
                (Data['result_title'].str.contains(phrasedefault3_7b, na=False, case=False))&
                (Data['result_title'].str.contains(phrasedefault3_7c, na=False, case=False))
               )  
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

```
TS =
(
  ("reproductive health" OR "sexual health" OR "reproductive healthcare" OR "sexual healthcare"
  OR "family planning" OR "planned pregnanc*" OR "contracept*" OR "abortion$"
  OR (("reproduct*" OR "sex*" OR "STI") NEAR/5 ("education" OR "inform*" OR "health literacy"))
  )
  NEAR/15
    (
      ("policy" OR "policies" OR "initiative$" OR "framework$" OR "program*" OR "strateg*")
      NEAR/5
          ("national" OR "state" OR "federal"
          OR ***LMICS***
          )
    )
)
```



```python
#Termlists  
termlist3_7e = ["reproductive health", "sexual health", "family planning", "planned pregnanc", "contracept", "abortion",
                "reproduksjonshelse", "reproduktiv helse", "seksuell helse", "familieplanlegging", "planlagt graviditet", "prevensjon", "abort"]
termlist3_7f = ["reproduct", "sex", 
                "reproduk"]
termlist3_7g = ["education", "inform", "health literacy", 
                "utdann", "opplær", "opplys", "kompetanse"]
termlist3_7h = ["policy", "policies", "initiativ", "framework", "program",
                "strateg", "politikk", "retningslin", "rammeverk"]
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
       |
         (
            (Data['result_title'].str.contains(phrasedefault3_7f, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault3_7g, na=False, case=False))
         )
    )
    & (Data['result_title'].str.contains(phrasedefault3_7h, na=False, case=False))
    & ((Data['LMICs']==True)|(Data['result_title'].str.contains(phrasedefault3_7i, na=False, case=False)))
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


```
TS =
(
  ("universal health coverage" OR "universal healthcare" OR "universal health care")
)
```


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

#### Phrase 2


```
TS =
(
  ("health care" OR "healthcare" OR "health service$" OR "medical service$" OR "medical care" OR "health coverage"
  OR "family planning" OR "reproductive health" OR "sexual health" OR "reproductive healthcare" OR "sexual healthcare"
  OR "vaccine$" OR "immuni$ation"
  OR (("essential" OR "basic" OR "life saving" OR "necessary" OR "emergency") NEAR/3 ("medicines" OR "medication$" OR "treatment*" OR "therap*"))
  OR "treatment access" OR "access to treatment$"
  )
  NEAR/15
      ("health equity" OR "equity in health*" OR "health care equity" OR "equity in healthcare" OR "health for all" OR "vaccine equity"
      OR "access*" OR "barrier$" OR "obstacle$"
      OR "afford" OR "affordab*" OR "low cost" OR "inexpensive" OR "free service$" OR "free of charge" OR "voucher$"
      OR "unaffordab*" OR "high price$" OR "costly" OR "debt" OR "financial risk$" OR "financial burden$" OR "financial hardship" OR "household expenditure$" OR "medical expenditure$" OR "medical expenses" OR "medical bill$" OR "medical cost$" OR "out of pocket"
      OR "microinsurance"
      OR "quality medicines" OR "quality care" OR "quality of care" OR "quality health care"
      )
)
```



```python
#Termlists
termlist3_8b = ["health care", "healthcare", "health service", "medical service", "medical care", "health coverage", "family planning", "reproductive health", "sexual health",
                "vaccin", "immunisation", "immunization", "treatment access", "access to treatment",
                
                "helsehjelp", "helsetjeneste", "helseteneste", "omsorgstjeneste", "omsorgsteneste", "helsedekning", "familieplanlegging", "reproduksjonshelse", "reproduktiv helse", 
                "seksuell helse", "vaksine", "immunisering", "tilgang til behandling"]
termlist3_8c = ["essential", "basic", "life saving", "necessary", "emergency",
                "essensiell", "nødvendig", "grunnlegg", "livred", "nødvendig", "naudsynt", "nødstilfelle", "naudstilfelle"]
termlist3_8d = ["medicines", "medication", "treatment", "therap",
                "medisin", "behandl", "terap"]
termlist3_8e = ["health equity", "equity in health", "health care equity", "equity in healthcare", "health for all", "vaccine equity", "access", "barrier", "obstacle", 
                "afford", "low cost", "inexpensive", "free service", "free of charge", "voucher", "high price", "costly", "debt", "financial risk", "financial burden",
                "financial hardship", "household expenditure", "medical expenditure", "medical expenses", "medical bill", "medical cost", "out of pocket", "microinsurance",
                "quality medicines", "quality care", "quality of care", "quality health care",

                "rettferdig helse", "rettferdig vaksine", "tilgang", "adgang", "åtgang", "hindr", "hinder", "rimelig", "rimeleg", "billig", "billeg", "gratis", "høy pris", "høg pris",
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
        (Data['result_title'].str.contains(phrasedefault3_8b, na=False, case=False)) |
      (
        (Data['result_title'].str.contains(phrasedefault3_8c, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault3_8d, na=False, case=False)) 
      ) 

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
```
TS =
(
  ("air pollution" OR "PM2.5" OR "PM10" OR "particulate matter" OR "ozone"
  OR
    (
      ("nitrogen dioxide" OR "sulfur dioxide" OR "sulphur dioxide" OR "carbon monoxide" OR "volatile organic compounds")
      NEAR/15 ("pollution" OR "poisoning$")
    )
  OR "smoke pollution" OR "secondhand smok*" OR "second hand smok*" OR "involuntary smoking" OR "passive smoking"
  OR
    (         
      ("drinking water" OR "potable water" OR "water source$")
      NEAR/3 ("unsafe" OR "safe" OR "contaminated" OR "contamination" OR "pollut*" OR "clean")
    )
  OR "poor hygiene" OR "good hygiene" OR "hand hygiene" OR "personal hygiene" OR "hygiene practice$" OR "hygiene intervention$"
  OR "handwashing"
  OR "poor sanitation" OR "*adequate sanitation" OR "good sanitation" OR "sanitation facilities"
  OR "water, sanitation and hygiene"
  OR
    (
      ("food" OR "foods")
      NEAR/3 ("unsafe" OR "contaminated" OR "contamination" OR "sanitation")
    )
  OR "food poisoning$" OR "foodborne pathogens"
  OR ("poisoning$" NEAR/3 ("unintentional" OR "accidental"))
  )
  NEAR/15
      ("mortality" OR "death$" OR "illness*" OR "disease$" OR "morbidity" OR "poisoning$")
)      

```


```python
#Termlists
termlist3_9a = ["air pollution", "particular matter", "ozon", 
                "luftforurensing", "luftforurensning", "luftforureining", "partik"]
termlist3_9b = ["PM2.5", "PM10"]
termlist3_9c = ["nitrogen dioxide", "sulfur dioxide", "sulphur dioxide", "carbon monoxide", "volatile organic compounds",
                "nitrogendioksid", "svoveldioksid", "karbonmonoksid", "flyktig organisk forbindelse", "flyktige organiske forbindelse"]
termlist3_9d = ["pollution", "poisoning", 
                "forurensing", "forurensning", "forureining", "forgift" ]
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
        |
           (
             (Data['result_title'].str.contains(phrasedefault3_9c, na=False, case=False))
             &(Data['result_title'].str.contains(phrasedefault3_9d, na=False, case=False))
           )
        |(Data['result_title'].str.contains(phrasedefault3_9e, na=False, case=False))
        |
            (
                (Data['result_title'].str.contains(phrasedefault3_9f, na=False, case=False))
                &(Data['result_title'].str.contains(phrasedefault3_9g, na=False, case=False)) 
            )
        |(Data['result_title'].str.contains(phrasedefault3_9h, na=False, case=False))       
        | 
            (
                (Data['result_title'].str.contains(phrasedefault3_9i, na=False, case=False)) 
                &(Data['result_title'].str.contains(phrasedefault3_9j, na=False, case=False))
            )
        |(Data['result_title'].str.contains(phrasedefault3_9k, na=False, case=False)) 
        |
            (
                (Data['result_title'].str.contains(phrasedefault3_9l, na=False, case=False))
                &(Data['result_title'].str.contains(phrasedefault3_9m, na=False, case=False))
            )
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

```
TS =
(
  (
    ("hazardous chemical$" OR "hazardous material$" OR "hazardous substance$" OR "hazardous waste$"
    OR "pollution"
    OR "soil contamination" OR "contamination of soil$" 
    OR "water contamination" OR "contamination of water"
    OR "arsenic"
    OR "asbestos"
    OR "benzene"
    OR "cadmium"
    OR "dioxin$"
    OR "mercury"
    OR "fluoride"
    OR "pesticide$"
    OR "lead poison*" OR "lead *toxicity" OR "lead mediated *toxicity" OR "lead induced *toxicity" OR "lead exposure" OR "lead carcinogen*" OR "blood lead"
    OR "radioactive waste$"
    OR "persistent organic pollutant$"
    OR "sanitation"
    )
    NEAR/15
        ("mortality" OR "death$" OR "illness*" OR "disease$" OR "morbidity"
        OR "*toxicity" OR "poisoning$" OR "poisoned" OR "fluorosis"
        )
  )
  AND
      ("humans" OR "humanity" OR "human" OR "people" OR "person$"
        OR "children" OR "child" OR "under fives" OR "infant$" OR "toddler$" OR "babies" OR "teenager$" OR "adolescent$" OR "girls" OR "boys"
        OR "elderly" OR "adult$" OR "women" OR "men" OR "woman" OR "man" OR "girls" OR "boys"
        OR "rural" OR "urban" OR "city" OR "cities" OR "town$" OR "village$" OR "countr*" OR "nation$" OR "develop* state$"
        OR "patient$" OR "hospital*"
        OR "premature death$" OR "premature mortality"
        OR "neglected tropical disease$" OR "diarrhoea*" OR "diarrhea*"
      )
)
```

In this search it proved hard to exclude noise eg. from articles concerning animals. We could not use "human" terms to delimit the search as we did in Web of Science, as this excluded too many relevant hits. Sometimes articles which have animal names in the title, are ultimately concerned with issues relating to human conditions, therefore they shoud be included. It is also hard to specify species to include/exclude, as we cannot know or predict which may be used in what context.


```python
#Termlists
termlist3_9o = ["hazardous chemical", "hazardous material", "hazardous substance", "hazardous waste", "pollution", "soil contamination", "contamination of soils", "water contamination",
                "contamination of water", "arsenic", "asbestos", "benzen", "cadmium", "dioxin", "mercury", "fluoride", "pesticide", "lead poison", "lead toxicity", "lead mediated toxicity",
                "lead induced toxicity", "lead exposure", "lead carcinogen", "blood lead", "radioactive waste", "persistent organic pollutant", "sanitation",

                "farlige kjemikalier", "farlege kjemikaliar", "farlige materialer", "farlege materialar", "farlige stoff", "farlege stoff", "farlig avfall", "farleg avfall", "forurensing",
                "forurensning", "forureining", "forurenset grunn", "forureina grunn", "arsenikk", "asbest", "kadmium", "dioksin", "kvikksølv", "fluor", "pesticid", "blyforgift", 
                "blyeksponering", "radioaktivt avfall"
               ]

termlist3_9p = ["mortality", "death", "illness", "disease", "morbidity", "toxicity", "poisoning", "poisoned", "fluorosis",
                "dødelighet", "dødelegheit", "død", "daud", "sykdom", "sjukdom", "toksisitet", "gift", "forgift", "fluorose"
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

```
TS = ("Framework convention on tobacco control" OR "WHO FCTC")
```



```python
#Termlists
termlist3_a1 = ["framework convention on tobacco control", 
                "tobakkskonvensjon", "Verdens helseorganisasjons rammekonvensjon om forebygging av tobakksskad"]
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

```
TS =
(
  (
    (
      ("tobacco" OR "smoking" OR "cigarette$")
      NEAR/5
          ("reduc*" OR "control" OR "ban" OR "bans" OR "banning" OR "prohibiting" OR "prohibit"
          OR "legislation" OR "policy" OR "policies" OR "regulat*" OR "law" OR "strateg*" OR "intervention$"
          OR "tax" OR "taxes" OR "taxation"
          OR "health warning$"
          OR "smoking cessation" OR "quitting" OR "services" OR "cessation service" OR "cessation program*" OR "alternative$"
          )
    )
  OR "reduc* tobacco" OR "reduc* smoking" OR "decreas* tobacco"
  OR "reduce dependence on"
  )
  AND ("tobacco")
)
```



```python
#Termlists
termlist3_a3 = ["tobacco", "smoking", "cigarette", 
                "tobakk", "røyking", "sigarett"]
termlist3_a4 = ["reduc", "control", "ban", "prohibit", "legislation", "policy", "policies", "regulat", "law", "strateg", "intervention", "tax", "health warning",
                "smoking cessation", "quitting", "services", "cessation service", "cessation program", "alternativ"
                
                "reduser", "reduksjon", "kontroll", "forby", "forbud", "forbod", "lovgivning", "lovgiving", "politikk", "retningslin", "reguler", "lov", "strategi", "intervensjon", "inngrip",
                "skatt", "helseadvarsel", "helseåtvaring", "røykeslutt", "røykestopp", "slutt", "stopp", "tjeneste", "teneste"]
termlist3_a5 = ["reduce tobacco", "reduce smoking", "decrease tobacco", "reduce dependence on tobacco", 
                "redusere avhengig"]    
termlist3_a6 = ["tobacco", 
                "tobakk"]            

phrasedefault3_a3 = r'(?:{})'.format('|'.join(termlist3_a3))
phrasedefault3_a4 = r'(?:{})'.format('|'.join(termlist3_a4))
phrasedefault3_a5 = r'(?:{})'.format('|'.join(termlist3_a5))
phrasedefault3_a6 = r'(?:{})'.format('|'.join(termlist3_a6))
```


```python
Data.loc[(
              (
                (Data['result_title'].str.contains(phrasedefault3_a3, na=False, case=False))&
                (Data['result_title'].str.contains(phrasedefault3_a4, na=False, case=False))
              )
              |
                (Data['result_title'].str.contains(phrasedefault3_a5, na=False, case=False))             
    ),"tempsdg03_a"] = "SDG03_0a"

print("Number of results = ", len(Data[(Data.tempsdg03_a == "SDG03_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg03_a == "SDG03_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```
TS=
(
  ("tobacco farm*" OR "tobacco production" OR "tobacco growing" OR "tobacco grower$")
  AND
    ("diversif*" OR "alternative crop$" OR "crop substitution"
    OR "alternative livelihood$" OR "alternative sustainable livelihood$"
    )
)
```



```python
#Termlists 
termlist3_a7 = ["tobacco farm", "tobacco production", "tobacco growing", "tobacco grower", 
                "tobakksproduksjon", "produksjon av tobakk", "tobakksdyrk", "dyrking av tobakk", "tobakksbonde", "tobakksbønder"]
termlist3_a8 = ["alternativ", "diversif", "alternative crop", "crop substitution", "alternative livelihood", "alternative sustainable livelihood",
                "divers", "alternativt jordbruk", "alternativ avling", "alternativt levebrød", "alternative inntektsk", "bærekraftig levebrød", "berekraftig levebrød"]

phrasedefault3_a7 = r'(?:{})'.format('|'.join(termlist3_a7))
phrasedefault3_a8 = r'(?:{})'.format('|'.join(termlist3_a8))
```


```python
#search
Data.loc[(
        (Data['result_title'].str.contains(phrasedefault3_a7, na=False, case=False))&
        (Data['result_title'].str.contains(phrasedefault3_a8, na=False, case=False))
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

```
TS =
(
  (
    ("develop*" OR "research*" OR "R&D" OR "novel" OR "new")
    NEAR/5 ("medicine$" OR "medication$" OR "therapy" OR "therapies" OR "therapeutic$" OR "vaccin*" OR "drug$" OR "cures" OR "treatment$")
  )
  AND
    ("neglected tropical disease$"
    OR "buruli ulcer"
    OR "chagas"
    OR "dengue"
    OR "chikungunya"
    OR "dracunculiasis" OR "guinea-worm disease"
    OR "echinococcosis"
    OR "foodborne trematodiases"
    OR "human african trypanosomiasis" OR "sleeping sickness"
    OR "leishmaniasis"
    OR "leprosy"
    OR "lymphatic filariasis"
    OR "mycetoma" OR "chromoblastomycosis" OR "deep mycoses"
    OR "onchocerciasis" OR "river blindness"
    OR "rabies"
    OR "scabies"
    OR "schistosomiasis"
    OR "soil-transmitted helminthias*" OR "hookworm$" OR "roundworm$" OR "whipworm$" OR "Ascaris lumbricoides" OR "Trichuris trichiura" OR "Necator americanus" OR "Ancylostoma duodenale"
    OR "snakebite envenoming"
    OR "taeniasis" OR "cysticercosis"
    OR "trachoma"
    OR "yaws"
    OR ***LMICS***
    )
)
```



```python
#Termlists
termlist3_b1 = ["develop", "research", "r&d",
                "utvikl", "forskning", "FOU"]
termlist3_b1a = ["new", "novel", 
                 " ny"]
termlist3_b2 = ["medicine", "medication", "therap", "vaccin", "drug", "cures", "treatment", 
                "medisin", "medikament", "terap", "vaksin", "legemid", "behandl"]
#We tried two approaches here; one where "new" and "medicine" were separate. But this was noisy. Therefore we use those below.
termlist3_b2a = ["new medicine", "novel medicin", "new medicatio", "novel medication", "new therap", "novel therap",
                 "new vaccin", "novel vaccin", "vaccine development",
                 "new drug", "novel drug", "new cure", "novel cure", "new treatment", "novel treatment",

                 "ny medisin", "nytt medikament", "nye medikament", "ny terap",
                 "ny vaksine", "vaksineutvikling", "utvikling av vaksin", "nytt legemiddel", "nye legemid",
                 "ny behandling"]
termlist3_b3 = ["neglected tropical disease", "buruli ulcer", "chagas", "dengue", "chikungunya", "dracunculiasis", "guinea-worm disease", "echinococcosis", "foodborne trematodiases",
                "human african trypanosomiasis", "sleeping sickness", "leishmaniasis", "leprosy", "lymphatic filariasis", "mycetom", "chromoblastomycosis", "deep mycoses",
                "onchocerciasis", "river blindness", "rabies", "scabies", "schistosomiasis", "soil-transmitted helminthiasis", "hookworm", "roundworm", "whipworm", "ascaris lumbricoides",
                "trichuris trichiura", "necator americanus", "ancylostoma duodenale", "snakebite envenoming", "taeniasis", "cysticercosis", "trachoma", "yaws",
                
                "neglisjert tropesykdom", "neglisjerte tropesykdom", "neglisjert tropesjukdom", "neglisjerte tropesjukdom", "burulisår", "ekinokkokose", "trematodeinfeksjon",             
                "afrikansk trypanosomiasis", "lepra", "lymfatisk filariasis", "mykose", "kromomykose",
                "onkocerkose", "skabb", "helmintiasis", "jordoverført helminthiasis", "hakeorm", "rundorm", "guineaorm", 
                "trichuris", "necator", "ancylostoma", "taeniainfeksjon", "cysticerkose", "trakom", "frambøsi",
                
                "virus", "epidemi", "pandemi", "infectious", "communicable", 
                "smittsom", "overførbar",
                ]
 #a few general terms ("virus", "epidemi" etc.) not originally included in the Web of Science were added to termlist3_b3 
 #as very few hits resulted from the title search when using only the names of specific diseases

phrasedefault3_b1 = r'(?:{})'.format('|'.join(termlist3_b1))
phrasespecific3_b1a = r'\b(?:{})\b'.format('|'.join(termlist3_b1a))
phrasedefault3_b2 = r'(?:{})'.format('|'.join(termlist3_b2))
phrasedefault3_b2a = r'(?:{})'.format('|'.join(termlist3_b2a))
phrasedefault3_b3 = r'(?:{})'.format('|'.join(termlist3_b3))
```


```python
#Search 1 - in LMICs data
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_b2a, na=False, case=False))
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

```
TS =
(
  ("Doha declaration" OR "compulsory licens*" OR "patents" OR "intellectual property" OR "TRIPS agreement")
  AND
    ("pharmaceuticals" OR "medicine$" OR "vaccine$" OR "immuni$ation" OR "essential drug$" OR "medication$"
    OR (("essential" OR "life saving" OR "emergency" OR "health" OR "medical") NEAR/3 ("treatment*" OR "therap*"))
    OR "treatment access" OR "access to treatment$"
    )
  AND
    ("access" OR "accessibility"
    OR "affordab*" OR "low cost" OR "inexpensive" OR "free of charge" OR "unaffordab*" OR "expensive"
    )
)
OR TS=("vaccine equity" OR "vaccine inequity")
```



```python
#Termlists
termlist3_b4 = ["doha declaration", "compulsory licens", "patent", "intellectual property", "TRIPS agreement",
                "doha-erklæring", "tvangslisens", "immaterielle rett", "intellektuell eiendom", "TRIPS-avtal"]
termlist3_b5 = ["pharmaceuticals", "medicine", "vaccine", "immunisation", "immunization", "essential drug", "medication", "treatment access", "access to therapy", 
                "legemid", "medisin", "vaksine", "immunisering", "essensiell medisin", "livsnødvendig medisin", "behandlingstilgang", "tilgang til behandling",
                "adgang til behandling", "åtgang til behandling"]
termlist3_b6 = ["essential", "life saving", "life-saving", "emergency", "health", "medical",
                "essensiel", "livred", "livsviktig", "krise", "akutt", "helse", "medisinsk"]
termlist3_b7 = ["treatment", "therapy", 
                "behandling", "terapi"]
termlist3_b8 = ["access", "affordab", "low cost", "low-cost", "inexpensive", "free of charge", "expensive", 
                "tilgang", "adgang", "åtgang", "rimelig", "rimeleg", "billig", "billeg", "gratis"]
termlist3_b9 = ["vaccine equity", "vaccine inequity", 
                "vaksinefordeling", "fordeling av vaksiner"]

phrasedefault3_b4 = r'(?:{})'.format('|'.join(termlist3_b4))
phrasedefault3_b5 = r'(?:{})'.format('|'.join(termlist3_b5))
phrasedefault3_b6 = r'(?:{})'.format('|'.join(termlist3_b6))
phrasedefault3_b7 = r'(?:{})'.format('|'.join(termlist3_b7))
phrasedefault3_b8 = r'(?:{})'.format('|'.join(termlist3_b8))
phrasedefault3_b9 = r'(?:{})'.format('|'.join(termlist3_b9))
```


```python
#Search 2

Data.loc[(
      (
          (
          (Data['result_title'].str.contains(phrasedefault3_b4, na=False, case=False)) &
          (Data['result_title'].str.contains(phrasedefault3_b5, na=False, case=False))
          )
          |
          (Data['result_title'].str.contains(phrasedefault3_b9, na=False, case=False))
      )
      |
         (
          (
             (Data['result_title'].str.contains(phrasedefault3_b5, na=False, case=False)) |
               (
                  (Data['result_title'].str.contains(phrasedefault3_b6, na=False, case=False))&
                  (Data['result_title'].str.contains(phrasedefault3_b7, na=False, case=False))  
               ) 
          )
            &
            (Data['result_title'].str.contains(phrasedefault3_b8, na=False, case=False))
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

```
TS =
(
  (
    (
      ("recruitment" OR "professional development" OR "retention" OR "capacity building" OR "capacity development"
      OR "increase training" OR "improv* training" OR "enhanc* training"
      OR "increase education" OR "improv* education" OR "enhanc* education"
      OR "train more" OR "recruit more" OR "increase trained" OR "increase the number of"
      OR "human capital flight" OR "brain drain" OR "emigration" OR "turnover" OR "intention to leave"
      )
    )
    NEAR/15
        (
           (
             ("health" OR "healthcare" OR "medical")
             NEAR/3 ("workforce" OR "professional$" OR "worker$" OR "personnel" OR "practitioner$" OR "human resources" OR "student$")
           )
           OR "nurse$" OR "doctor$" OR "physician$"
           OR "Anesthetist$" OR "Audiologist$" OR "Dental Staff" OR "Dentist$" OR "Doula$" OR "Emergency Medical Dispatcher$" OR "Health Educator$" OR "Health Facility Administrator$" OR "Infection Control Practitioner$" OR "Medical Chaperone$" OR "Medical Laboratory Personnel" OR "Nutritionist$" OR "Therapist$" OR "Optometrist$" OR "Pharmacist$" OR "Allergist$" OR "Anesthesiolog*" OR "Cardiolog*" OR "Dermatolog*" OR "Endocrinolog*" OR "Gastroenterolog*" OR "General Practic*" OR "Geriatrician$" OR "gynecologist$" OR "Hospitalist$" OR "Nephrolog*" OR "Neurolog*" OR "Oncolog*" OR "Ophthalmolog*" OR "Otolaryngolog*" OR "midwives" OR "Pathologist$" OR "Pediatric*" OR "Physiatrist$" OR "Pulmonolog*" OR "Radiolog*" OR "Rheumatolog*" OR "surgeon$" OR "Urologist$"
       )
  )
  AND
      (***LMICs***   
      )
)
```



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
            |
            (
                (Data['result_title'].str.contains(phrasedefault3_c2, na=False, case=False))
                & (Data['result_title'].str.contains(phrasedefault3_c3, na=False, case=False))
            )
        )
        & 
        (
            ( 
                (Data['result_title'].str.contains(phrasedefault3_c4, na=False, case=False))
                & (Data['result_title'].str.contains(phrasedefault3_c5, na=False, case=False))
            )
            | (Data['result_title'].str.contains(phrasedefault3_c6, na=False, case=False))
        )    
    )
    &(Data['LMICs']==True)
),"tempsdg03_c"] = "SDG03_c"

print("Number of results = ", len(Data[(Data.tempsdg03_c == "SDG03_c")]))  
```

#### Phrase 2


```
TS =
(
  (
    ("financing" OR "invest" OR "investment$" OR "investing" OR "funding" OR "funds"
    OR "health spending" OR "health care spending" OR "health budget" OR "public spending" OR "government spending"
    OR "financial assist*" OR "economic assist*" OR "financial support" OR "financial resources"
    OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
    OR "ODA" OR "cooperation fund$" OR "development spending"
    OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance" OR "finance" OR "grant$"))
    )
    NEAR/15
        ("health sector" OR "health financing" OR "health budget" OR "health spending"
        OR "health service$" OR "healthcare" OR "health care" OR "medical care"
        OR "medical research" OR "health research" OR "health R&D" OR "medical R&D"
        )   
  )
  AND
    (****LMICs****)
)
```




```python
#Termlists
termlist3_c8 = ["financing", "invest", "fund", "health spending", "health care spending", "health budget", "public spending", "government spending",
                "financial assist", "economic assist", "financial support", "financial resources", "subsidy", "subsidies", "subsidis", "subsidiz",
                "ODA", "cooperation fund", "development spending",

                "finansie", "fond", "helseutgift", "helsebudsjett", "offentlige utgifter", "offentlege utgifter", "finansiell assistanse", "økonomisk assistanse", 
                "finansiell støtte", "finansiell stønad", "finansielle ressurs", "subsidi", "offentlig utviklings", "offentleg utviklings", "offisiell utviklings", "samarbeidsfond"
               ]
termlist3_c9 = ["international", "development", "foreign", 
                "internasjonal", "utvikling", "utenlands", "utanlands"
               ]
termlist3_c10 = ["aid", "assistance", "finance", "grant", 
                 "hjelp", "støtte", "stønad", "bistand", "assistanse", "finansie"
                ]
termlist3_c11 = ["health sector", "health financing", "health budget", "health spending", "health service", "healthcare", "health care", "medical care",
                 "medical research", "health research", "health R&D", "medical R&D",
                 "helsesektor", "helsefinansiering", "helsebudjett", "helseøkonomi", "helseutgift", "helsetjeneste", "helseteneste", "omsorgstjeneste", "omsorgsteneste", 
                 "medisinsk forskning", "medisinsk forsking", "helseforskning", "helseforsking"
                ]

phrasedefault3_c8 = r'(?:{})'.format('|'.join(termlist3_c8))
phrasedefault3_c9 = r'(?:{})'.format('|'.join(termlist3_c9))
phrasedefault3_c10 = r'(?:{})'.format('|'.join(termlist3_c10))
phrasedefault3_c11 = r'(?:{})'.format('|'.join(termlist3_c11))

```


```python
#Search - in LMICs data
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault3_c8, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasedefault3_c9, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault3_c10, na=False, case=False))
        )
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

#### Phrase 1

```
TS =
(
  (
    ("national health risk$" OR "international health risk$" OR "global health risk$"
    OR "pandemic$" OR "epidemic$" OR "outbreak$"
    OR "medical disaster$" OR "health emergency" OR "health emergencies"
    OR "radiation emergenc*" OR "radiation event$"
    OR "chemical event$" OR "chemical emergenc*"
    OR "zoonotic event$" OR "zoonotic emergenc*"
    OR "food safety" OR "foodborne event$"
    OR "biosecurity event$" OR "biosecurity emergenc*"
    OR "antimicrobial resistan*" OR "antibiotic resistan*" OR "antifungal resistan*"
    )
    NEAR/15  
      ("capacity" OR "early warning*" OR "surveillance" OR "monitoring system$"
      OR "laboratory reporting" OR "laboratory infrastructure" OR "laboratory quality" OR "laboratory system$"
      OR "preparedness" OR "medical preparedness" OR "disaster planning" OR "national health emergency framework" OR "emergency risk assessment$"
      OR "risk reduction" OR "risk management" OR "risk communication"
      OR "emergency management" OR "emergency response" OR "personnel deployment" OR "security authorities"
      OR "vaccination program*" OR "vaccination framework$" OR "immuni$ation program*"
      OR "legislation" OR "policy" OR "policies" OR "financing"
      OR "international health regulations" OR "national focal point$" OR "national action plan*"
      )
  )
  NOT
      ("blight" OR "plant pathogen$" OR "plant disease$")
)
```




```python
#Termlists
termlist3_d1 = ["national health risk", "global health risk", "pandemi", "epidemic", "outbreak", "medical disaster", "health emergenc", "radiation emergenc", "radiation event"
                "chemical event", "chemical emergenc", "zoonotic event", "zoonotic emergenc", "food safety", "foodborne event", "biosecurity event", "biosecurity emergenc"
                "antimicrobial resistan", "antibiotic resistan", "antifungal resistan",
                
                "helserisiko", "epidemisk", "epidemier", "epidemien", "utbrudd", "utbrot", "medisinsk katastrofe", "strålingsulykke", 
                "kjemikalieulykke", "zoonotisk", "matsikkerhe", "matbåren", "biosikkerhe", "antimikrobiell resistens",
                "antibiotikaresistens", "antimykotisk"]  
termlist3_d1trunk = ["epidemi"]                
termlist3_d2 = ["capacity", "early warning", "surveillance", "monitoring system", "laboratory reporting", "laboratory infrastructure", "laboratory quality", "laboratory system",
                "preparedness", "disaster planning", "national health emergency framework", "emergency risk assessment", "risk reduction", "risk management", "risk communication",
                "emergency management", "emergency response", "personnel deployment", "security authorities", "vaccination program", "vaccination framework", "immunisation program", 
                "immunization program", "legislation", "polic", "financing", "international health regulation", "national focal point", "national action plan",
                
                "kapasitet", "tidligvarsling", "tidlig varsling", "tidlegvarsling", "tidleg varsling", "overvåk", "overvaking", "laboratorie", 
                "forberedt", "førebudd", "katastrofeplan", "kriseplan", "nasjonal helseberedskapsplan", "risikovurdering", "risikoreduksjon", "risikohåndtering", "risikokommunikasjon", 
                "krisehåndtering", "kriserespons", "sikkerhetsmyndighet", "tryggingsorgan", "vaksinasjonsprogram", "vaksinasjonsrammeverk", "immuniseringsprogram",
                "lovgivning", "lovgiving", "politikk", "retningslin", "finansiering", "internasjonalt helsereglement", "internasjonale helsereglement", "nasjonal handlingsplan"]
termlist3_d3 = ["blight", "plant pathogen", "plant disease" ]       
# for a title search, it was not necessary to exlude the terms in termslist 3_d3 with a NOT search         

phrasedefault3_d1 = r'(?:{})'.format('|'.join(termlist3_d1))
phrasespecific3_d1trunk = r'\b(?:{})\b'.format('|'.join(termlist3_d1trunk))
phrasedefault3_d2 = r'(?:{})'.format('|'.join(termlist3_d2))
phrasedefault3_d3 = r'(?:{})'.format('|'.join(termlist3_d3))
```


```python
#search
Data.loc[(
     (
         (Data['result_title'].str.contains(phrasedefault3_d1, na=False, case=False))|
         (Data['result_title'].str.contains(phrasespecific3_d1trunk, na=False, case=False))
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

```
TS=
("SDG 3" OR "SDGs 3" OR "SDG3" OR "sustainable development goal$ 3"
OR ("sustainable development goal$" AND "goal 3")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 3")
    NEAR/50 ("health")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  OR (("soil health" OR "ecosystem health" OR "coastal health" OR ("ocean$" NEAR/5 "health")) NOT ("human health"))
  )
  ```
 Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 


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
      (Data['result_title'].str.contains(phrasedefault3_1, na=False, case=False))|
        (
          (Data['result_title'].str.contains(phrasedefault3_2, na=False, case=False))&
          (Data['result_title'].str.contains(phrasedefault3_3, na=False, case=False))
        )
       |
       (
         (Data['result_title'].str.contains(phrasedefault3_4, na=False, case=False))&
         (Data['result_title'].str.contains(phrasedefault3_5, na=False, case=False))
       )
       |
       (Data['result_title'].str.contains(phrasedefault3_6, na=False, case=False))
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

```
TS=
(
 ("complete" OR "completing" OR "completes" OR "completion" OR "school completion" OR "finish*" OR "graduate" OR "graduation")
  NEAR/5
      ("primary school*" OR "elementary school*" OR "primary educat*"
      OR "middle school*" OR "secondary school*" OR "secondary education*"
      OR (("school" OR "education") NEAR/3 ("boys" OR "girls" OR "kids" OR "child*"))
      )
)


TS=
(
 ("dropout*" OR "drop-out*" OR "drop out" OR "dropping out" OR "quit" OR "early school-leaving")
   NEAR/5
      ("primary school*" OR "elementary school*" OR "primary educat*"
      OR "middle school*" OR "secondary school*" OR "secondary education*"
      OR (("school" OR "education") NEAR/3 ("boys" OR "girls" OR "kids" OR "child*"))
      )
)


TS=
(
 (
  ("access*" OR "enter*" OR "entry" OR "enroll*" OR "admission" OR "admit*")
  NEAR/15
   (
     ("primary school*" OR "elementary school*" OR "primary educat*"
        OR "middle school*" OR "secondary school*" OR "secondary education"
      )
      NEAR/5 ("free" OR "equit*" OR "quality")
    )
 )
)  


TS=
(
  (
    ("basic" OR "fundamental*" OR "minim*" OR "basic*" OR "core" OR "elementary")
    NEAR/10 
    ("proficienc*" OR "skill*" OR "comprehen*" OR "literac*" OR "read*" OR "mathematic*" OR "math" OR "maths" OR "numera*")
  )
    NEAR/15
    ("read" OR "reading" OR "mathematic*" OR "math" OR "maths" OR "numera*")
    AND 
    ("school" OR "student$" OR "boys" OR "girls" OR "kids" OR "child*")
)


```

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
        (
        (Data['result_title'].str.contains(phrasedefault4_1_1b, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_1_1e, na=False, case=False))
        )
    |
        (
         (Data['result_title'].str.contains(phrasedefault4_1_1c, na=False, case=False)) &
         (Data['result_title'].str.contains(phrasespecific4_1_1d, na=False, case=False))
         )
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
                  "droppe ut", "frafall", "fråfall", "falle ut"]
                 
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
        (Data['result_title'].str.contains(phrasedefault4_1_2a, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_1_2e, na=False, case=False))
    )
  & 
    (
        (
            (Data['result_title'].str.contains(phrasedefault4_1_2b, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_1_2f, na=False, case=False))
        )
        |
        (
            (Data['result_title'].str.contains(phrasedefault4_1_2c, na=False, case=True)) 
            & (Data['result_title'].str.contains(phrasespecific4_1_2d, na=False, case=False))
        )
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
        (Data['result_title'].str.contains(phrasedefault4_1_3a, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_1_3c, na=False, case=False))
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
                  "les", "regneferdigh", "rekneferdigh", "talforstå", "tallforstå", "talferdigh", "tallferdigh", "matematikk", "rekning", "regning"]

termlist4_1_4e = ["school", "student", "boys", "girls", "kids", "child", 
                  "skole", "skule", "gut", "jente", "born", "barn", "elever", "elevar" ]
                 
termlist4_1_4f = ["read"]
                                   
                 
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
          & (
              (Data['result_title'].str.contains(phrasedefault4_1_4b, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_1_4f, na=False, case=False))
            )
      )
      |(Data['result_title'].str.contains(phrasedefault4_1_4c, na=False, case=False))
    )
    & ((Data['result_title'].str.contains(phrasedefault4_1_4d, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific4_1_4f, na=False, case=False)))
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

```
Phrase 1:

TS=
(
 (
  ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*")
 )
  NEAR/5
      ("early childhood care" OR "kindergarten" OR "pre-kindergarten*" OR "nurser*" OR "pre-primary*" OR "pre school*" OR "preschool*"
      OR (("early childhood" OR "under five$") NEAR/3 "education")
  )
)
NOT
TS= ("pig*" OR "plant*" OR "fish*")

Phrase 2:
TS=
(
  "school readiness"
  OR
    (
      ("ready" OR "readiness" OR "prepared*")
      NEAR/5
        ("primary education*" OR "primary school*" OR "elementary school*" OR "first grade" OR "1st grade*")
    )
  OR
    (
      ("development*" NEAR/5 ("children*" OR "under-five*" OR "early childhood"))
      NEAR/5 "school entry"
   )
)


```


#### Phrase 1


```python
#Termlists
termlist4_2_1a = ["access", "obstacle", "barrier", "hinder", "hindrance", "equitab", "non-equit",  
                "tilgang", "adgang", "tilgjenge", "barrier", "hindring", "hinder", "hindre"
                ]


termlist4_2_1b = ["early childhood care", "kindergarten", "pre-kindergarten", "nurser", "pre-primary education", "pre school education", "preschool education", 
                  "førsk", "barnehage", "tidlig utvikling", "tidleg utvikling"
                ]

termlist4_2_1c = ["early childhood", "under five", "under-five"]

termlist4_2_1d = ["education"]

termlist4_2_1e = ["barnehagedekning", "barnehageplass", "tilbud om barnehage", "tilbod om barnehage", "barnehageopptak"]


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
        & (
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

termlist4_2_2b = ["ready", "readiness", "prepared", 
                 "moden", "mogen", "forberedt", "førebudd", "overgang"]
                                  
termlist4_2_2c = ["primary education", "primary school", "elementary school", "first grade", "1st grade", 
                "første klass", "fyrste klass", "6-åring", "seksåring", "fyrsteklass", "førsteklass", "skole", "skule", "barnehage"]

termlist4_2_2d = ["development", 
                "utvikling"]

termlist4_2_2e = ["child", "under-five", "early childhood",
                "barn", "tidlig barndom", "tidleg barndom"]
                
termlist4_2_2f= ["school entry",
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

```
TS=
(
  (
    ("access*" OR "inclusion*" OR "inclusiv*" OR "non-discriminat*" OR "equitab*" OR "equal*" OR "afford*")
    OR
    ("barrier$" OR "obstacle$" OR "non-equitiab*" OR "inequal*" OR "discriminat*")
  )
  NEAR/5
      ("higher education"
      OR 
       (("university" OR "universities" OR "college$") NEAR/5 ("admission$" OR "enrol*"))
      OR
        (("technic*" OR "vocation*" OR "tertiar*" OR "university" OR "postsecondary" OR "post secondary")
         NEAR/3 ("education" OR "training" OR "school*" OR "learning")
        )
     )
)


TS=
(
  (
    (
      ("inclusion*" OR "inclusiv*" OR "non-discriminat*" OR "equitab*" OR "equal*")
      OR
      (
       ("barrier$" OR "obstacle$" OR "non-equitiab*" OR "inequal*" OR "discriminat*")
      )
    )
    NEAR/15 ("access")
  )
  NEAR/15
      ("university" OR "universities" OR "higher education" OR "college$"
      OR
        (
          ("technic*" OR "vocation*" OR "tertiar*" OR "postsecondary" OR "post secondary")
          NEAR/3 ("education" OR "training" OR "school*" OR "learning")
        )
   )
)


TS= "inclusive higher education"




#### Phrase 1 & Phrase 2
Due to title search, phrase 1 and phrase 2 from WoS are here combined into one phrase. To a great extent, in WoS, the two phrases contain the same terms. We have included *Access* in termlist e) -  which is searched in AND-combination with termlist d) *University* - in order to include some more hits.



```python
#Termlists
termlist4_3_1a = ["access", "inclusion", "inclusiv", "equitab", "equal", "afford", "barrier", "obstacle", "discriminat",
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
        |(
            (Data['result_title'].str.contains(phrasedefault4_3_1d, na=False, case=False)) 
            & (Data['result_title'].str.contains(phrasedefault4_3_1e, na=False, case=False))
         )
        | 
         (
          (Data['result_title'].str.contains(phrasedefault4_3_1f, na=False, case=False)) 
            & (Data['result_title'].str.contains(phrasedefault4_3_1g, na=False, case=False))
         )
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

termlist4_3_3a = ["inclusive", "inclusion", "inkluder"]
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

```
TS=
(
  (
   ("skill$" OR "abilit*" OR "competenc*" OR "literac*")
  )
  NEAR/5
  ("employability*" OR "employment" OR "decent job$" OR "decent work" OR "entrepreneurship$")
)


TS=
(
  (
    ("unemploy*" OR "underemploy*")
  )
  NEAR/5 
  ("skill$" OR "abilit*" OR "competenc*" OR "literac*" OR "literate")
 )



 TS=
(
  (
    "read*" OR "writ*" OR "comput*" OR "literacy" OR "numeracy"
    OR (("basic technolog*" OR "speciali$ed") NEAR/3 ("skills" OR "knowledge"))
    OR "learn and adapt"
    OR (("listen*" OR "communicat*") NEAR/3 ("skills" OR "effective*"))
    OR "think creatively" OR "creative thinking" OR "solve problem$" OR "problem-solv*"
    OR ("interact*" NEAR/3 ("co-work*" OR "colleague$"))
    OR (("work" OR "working") NEAR/3 ("team*" OR "group*"))
    OR ("leader*" NEAR/5 ("skills" OR "effectiv*"))
    OR ("follow*" NEAR/3 "supervis*")
    OR ("transfer*" NEAR/3 "skills")
  )
  NEAR/15 "employability"
)



TS=
(
  (
   ("information and communication technology" OR "ICT" OR "vocational" OR "technical" OR "technolog*" OR "comput*" OR "data*" OR "digital*" OR "information")
    NEAR/5
    ("skill*" OR "competen*" OR "literac*")
  )
   NEAR/15
   ("employab*" OR "employment" OR "job$" OR "decent work")
)


``` 


#### Phrase 1


```python
#Termlists
termlist4_4_1a = ["skill", "abilit", "competenc", "literac"
                  "ferdigh", "kompetanse", "dugleik", "dyktighe",   
                ]
              
termlist4_4_1b = ["employability", "employment", "decent job", "decent work", "entrepreneurship",
                 "ansettelse", "sysselset", "tilset", "anstendig arbeid", "anstendig jobb", "jobb", "entreprenørskap" ]

phrasedefault4_4_1a = r'(?:{})'.format('|'.join(termlist4_4_1a))
phrasedefault4_4_1b = r'(?:{})'.format('|'.join(termlist4_4_1b))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_4_1a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_1b, na=False, case=False))
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
termlist4_4_2a = ["unemploy", "underemploy", 
                  "arbeidsledig", "langtidsledig", "arbeidslau", "arbeidslø", "utan arbeid", "uten arbeid", "utan jobb", "uten jobb",
                  "ikkje i arbeid", "ikke i arbeid"
                ]
              
termlist4_4_2b = ["skill", "abilit", "competenc", "litera", 
                  "ferdigh", "kompetanse", "evne", "dugleik", "dyktighe", "kyndig",]

phrasedefault4_4_2a = r'(?:{})'.format('|'.join(termlist4_4_2a))
phrasedefault4_4_2b = r'(?:{})'.format('|'.join(termlist4_4_2b))
```


```python
#Search 
phrase4_4_2 = Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_4_2a, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_2b, na=False, case=False))
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
    | ((Data['result_title'].str.contains(phrasedefault4_4_3b, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3c, na=False, case=False)))
    | (Data['result_title'].str.contains(phrasedefault4_4_3d, na=False, case=False))
    | ((Data['result_title'].str.contains(phrasedefault4_4_3e, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3f, na=False, case=False)))
    | (Data['result_title'].str.contains(phrasedefault4_4_3g, na=False, case=False))
    | (Data['result_title'].str.contains(phrasedefault4_4_3h, na=False, case=False))
    | ((Data['result_title'].str.contains(phrasedefault4_4_3i, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3j, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasedefault4_4_3k, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3l, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasedefault4_4_3n, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3f, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasedefault4_4_3o, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3p, na=False, case=False)))
    | ((Data['result_title'].str.contains(phrasedefault4_4_3q, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_4_3r, na=False, case=False)))
)
    & (Data['result_title'].str.contains(phrasedefault4_4_3s, na=False, case=False))
    ),"tempsdg04_04"] = "SDG04_04"

print("Number of results = ", len(Data[(Data.tempsdg04_04 == "SDG04_04")])) 
```


```python
test=Data.loc[(Data.tempsdg04_04 == "SDG04_04"), ("result_id", "result_title")]
test.iloc[20:25, ] 
```

#### Phrase 4


```python
#Termlists
termlist4_4_4a = ["information and communication technology", "ICT", "vocational", "technical", "technolog", "comput", "data", "digital", "information",
                  "informasjonsteknologi", "IKT", "fagsk", "teknisk", "teknologi"                   
                 ]

termlist4_4_4b = ["skill", "competen", "literac",
                  "ferdigh", "kompetanse", "evne", "dugleik", "dyktigh"]

termlist4_4_4c = ["it-kompetanse", "it-ferdigh", "ikt-kompetanse", "ikt-ferdigh", "datakompetanse", "dataferdigh",
                  "teknologikompetanse", "teknologiferdigh"]                  

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
    &
    (Data['result_title'].str.contains(phrasedefault4_4_4d, na=False, case=False))
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

```
TS=
(
 (
  ("gender" OR "girl*" OR "woman*" OR "women*" OR "female*" OR "boy$" OR "man" OR "men" OR "male")
   NEAR/5
   ("equit*" OR "equal*" OR "balanc*")
 ) 	
   NEAR/5 ("school*" OR "educat*" OR "vocational training" OR "student*")
)


TS=
(
 (
  ("gender" OR "girl*" OR "woman*" OR "women*" OR "female*" OR "boy$" OR "man" OR "men" OR "male")
   NEAR/5
   ("non-equit*" OR "non-equal*" OR "inequal*" OR "unequal*" OR "unbalanc*" OR "imbalanc*" OR "disparit*" OR "discriminat*"
    OR "obstacle*" OR "barrier*" OR "hindrance*" OR "hinder*")
  )
   NEAR/5
   ("school*" OR "educat*" OR "vocational training" OR "student*")
)


TS=
(
  (
    (
     ("access" OR "admission*" OR "admit*" OR "attend*" OR "entry" OR "enrol*" OR "inclusion*" OR "inclusiv*" OR "non-discriminat*" OR "equitab*")
      OR
      ("discriminat*" OR "non-discriminat*" OR "non-equit*" OR "disparit*"OR "barrier*" OR "obstacle*") 
    )
    NEAR/5 ("school*" OR "educat*" OR "vocational training")
  )
  NEAR/15
      (
        (
         ("person$" OR "people" OR "adult$" OR "child*" OR "student$" OR "youth$" OR "adolescent$")  
          NEAR/3
              ("disabled" OR "disabilit*" OR "unemployed" OR "older" OR "elderly"
              OR "poor" OR "poorest" OR "poverty" OR "disadvantaged" OR "vulnerab*" OR "displaced" OR "marginali$ed" OR "developing countr*")
        )
     OR "disab*" OR "disadvantage*" OR "vulnerab*" OR "indigenous" OR "the poor" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
     OR "refugee$" OR "asylum*" OR "displaced" OR "migrant*" OR "low* income*" OR "minorit*"  OR "marginal*" OR "slum*" OR "rural"
     )
)


```


#### Phrase 1


```python
#Termlists
termlist4_5_1a = ["gender", "girl", "woman", "women", "female", "boy", "male",
                "kjønn", "jente", "kvinne", "gut"
                ]

termlist4_5_1b = ["equit", "equal", "balanc",
                  "rettferd", "rettvis", "jevnbyrdig", "likheit", "likhet", "likskap", "ulikskap", "skilnad", "balans" 
                  ]
                 
termlist4_5_1c = ["likestilling"]

termlist4_5_1d = ["school", "educat", "vocational training", "student",
                  "skole", "skule", "utdann", "undervisning", "undervising", "opplæring", "yrkesfag"
                  ]

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
    |
      (Data['result_title'].str.contains(phrasedefault4_5_1c, na=False, case=False))
    )
    & 
    (Data['result_title'].str.contains(phrasedefault4_5_1d, na=False, case=False))
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
                "kjønn", "jente", "kvinne", "gut"
                ]

termlist4_5_2b = ["non-equit", "non-equal", "inequal", "unequal", "unbalanc", "imbalanc", "disparit", "discriminat", 
                  "obstacle", "barrier", "hindrance", "hinder",
                  "ulikhet", "ulikheit", "urett", "ubalans", "misforhold", "forskjell", "skilnad", "diskriminer", "hinder", "hindre", "barrier"
                  ]

termlist4_5_2c = ["kjønnsdiskriminering", "kjønnsforskjell", "kjønnsskilnad"]

termlist4_5_2d = ["school", "educat", "vocational training", "student",
                  "skole", "skule", "utdann", "undervisning", "undervising", "opplæring", "yrkesfag"]

termlist4_5_2e = ["mortality", "health", "wealth"]

phrasedefault4_5_2a = r'(?:{})'.format('|'.join(termlist4_5_2a))
phrasedefault4_5_2b = r'(?:{})'.format('|'.join(termlist4_5_2b))
phrasedefault4_5_2c = r'(?:{})'.format('|'.join(termlist4_5_2c))
phrasedefault4_5_2d = r'(?:{})'.format('|'.join(termlist4_5_2d))
phrasedefault4_5_2e = r'(?:{})'.format('|'.join(termlist4_5_2e))
```


```python
#Search
Data.loc[(
    (
        (
         (Data['result_title'].str.contains(phrasedefault4_5_2a, na=False, case=False)) 
            & (Data['result_title'].str.contains(phrasedefault4_5_2b, na=False, case=False))
        )
        |(Data['result_title'].str.contains(phrasedefault4_5_2c, na=False, case=False)) 
    )
    & (Data['result_title'].str.contains(phrasedefault4_5_2d, na=False, case=False))
    & (~Data['result_title'].str.contains(phrasedefault4_5_2e, na=False, case=False))
),"tempsdg04_05"] = "SDG04_05"

print("Number of results = ", len(Data[(Data.tempsdg04_05 == "SDG04_05")]))  
```


```python
test=Data.loc[(Data.tempsdg04_05 == "SDG04_05"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3


```python
#Termlists
termlist4_5_3a = ["access", "admission", "admit", "attend", "entry", "enrol", "inclusion", "inclusiv", "non-discriminat", "equitab", 
                  "tilgang", "tilgjenge", "adkomst", "adgang", "opptak", "inkluder", "rettferd", "rettvis"
                  ]

termlist4_5_3b = ["discriminat", "non-discriminat", "non-equit", "disparit", "barrier", "obstacle",
                  "diskriminer", "urettvis", "urettferd", "barrier", "hinder", "hindr"
                  ]

termlist4_5_3c =  ["school", "educat", "vocational training", 
                  "skole", "skule", "utdann", "undervis", "opplæring", "yrkesfagl"
                  ]   

termlist4_5_3d =  ["person", "people", "adult", "child", "student", "youth", "adolescent",
                   "menneske", "vaksne", "voksne", "elev", "ung", "tenåring", "barn", "born"
                  ]        
                   
termlist4_5_3e = ["disabled", "disabilit", "unemployed", "older", "elderly", "poor", "poverty", "disadvantaged", "vulnerab", "displaced", "marginali", "developing countr",
                 "uføre", "funksjonshem", "arbeidsl", "utan arbeid", "uten arbeid", "fattig", "lavinntekt", "låginntekt", "lav inntekt", "låg inntekt", "sårbar", "diskriminert", 
                  "marginalisert", "utviklingsland", "u-land"]
                  #Norwegian terms for OLDER are not included as they cause noise.
                  
termlist4_5_3f = ["disab", "disadvantage", "vulnerab", "indigenous", "the poor", "LGBT", "lesbian", "gay", "bisexual", "transgender", "refugee", "asylum", 
                  "displaced", "migrant", "low income", "minorit", "marginal", "slum", "rural",
                  "uføre", "funksjonshem", "sårbar", "hjemløs", "heimlaus", "urfolk", "urbefolkning", "urinnvån", "minoritet", 
                  "sápmi", "sami", "minoritet", "jøder", "jådar", "kvener", "kvenar", "norskfinn", "skogfinn", "romani", "tatere", "taterar",
                  "asylsøk", "flyktning", "innvandr",
                  "fattig", "lavinntekt", "låg inntekt", "låginntekt", "lav inntekt", "slum", 
                  "transperson", "lesbisk", "homofile", "homoseksuell", "bifil", "lbht", "interkjønn", "innfød"]
                 
phrasedefault4_5_3a = r'(?:{})'.format('|'.join(termlist4_5_3a))
phrasedefault4_5_3b = r'(?:{})'.format('|'.join(termlist4_5_3b))
phrasedefault4_5_3c = r'(?:{})'.format('|'.join(termlist4_5_3c))
phrasedefault4_5_3d = r'(?:{})'.format('|'.join(termlist4_5_3d))
phrasedefault4_5_3e = r'(?:{})'.format('|'.join(termlist4_5_3e))
phrasedefault4_5_3f = r'(?:{})'.format('|'.join(termlist4_5_3f))
```


```python
#Search 
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault4_5_3a, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault4_5_3b, na=False, case=False)))
         & 
        (Data['result_title'].str.contains(phrasedefault4_5_3c, na=False, case=False))
    )
    &
    (
        ((Data['result_title'].str.contains(phrasedefault4_5_3d, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault4_5_3e, na=False, case=False)))
        |(Data['result_title'].str.contains(phrasedefault4_5_3f, na=False, case=False))
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

```
TS=
(
    (
      ("basic" OR "fundamental*" OR "minim*" OR "core" OR "elementary" OR "functional" OR "adequate*")
        NEAR/10 ("proficienc*" OR "skill*" OR "comprehen*" OR "abilit*" OR "literac*")
    )
    NEAR/5 ("read" OR "reading" OR "literate" OR "mathematic*" OR "math" OR "maths" OR "numeracy" OR "numerate")
)


TS=
 ("illitera*" OR "analfabet*" OR "analphabet*" OR "innumeracy" OR "innumerate*")
 ```

#### Phrase 1
The phrase is simplified compared to topic search in WoS. In order to get more hits, *level* is not included in the search. The syntax of the search is *skills + reading/mathematics*.



```python
#Termlists                
termlist4_6_1a = ["proficienc", "skill", "comprehension", "comprehend", "literac",  
                  "ferdigh", "dyktighe", "kyndighe", "kompetanse", "evne", "dugleik", "forstå"
                  ]

termlist4_6_1b = ["ability", "abilities"]

termlist4_6_1c =  ["reading", "literate", "mathematic", "maths", "mathematics", "numera", 
                  "leseferdigh", "leseforstå", "lesekompetanse", "lesedugleik", 
                   "rekne", "rekna", "regneferdigh", "rekneferdigh", "reknedugleik",
                   "talforstå", "tallforstå", "talferdigh", "tallferdigh", "matematikk"
                  ]  
termlist4_6_1d = ["read", "lese", "lesa", "lesing", "rekning", "regning"]                 

termlist4_6_1e = ["teacher", "readability", "readiness", "spread", "lærer", "lærar", "student", "skille", "mikropolitisk"]
                 #Noisy terms, removed with NOT

phrasedefault4_6_1a = r'(?:{})'.format('|'.join(termlist4_6_1a))
phrasespecific4_6_1b = r'\b(?:{})\b'.format('|'.join(termlist4_6_1b))
phrasedefault4_6_1c = r'(?:{})'.format('|'.join(termlist4_6_1c))
phrasespecific4_6_1d = r'\b(?:{})\b'.format('|'.join(termlist4_6_1d))
phrasedefault4_6_1e = r'(?:{})'.format('|'.join(termlist4_6_1e))
```


```python
#Search 
Data.loc[(
         (
             (Data['result_title'].str.contains(phrasedefault4_6_1a, na=False, case=False)) | 
             (Data['result_title'].str.contains(phrasespecific4_6_1b, na=False, case=False))
         )
         &
         (
             (Data['result_title'].str.contains(phrasedefault4_6_1c, na=False, case=False)) |
             (Data['result_title'].str.contains(phrasespecific4_6_1d, na=False, case=False))
         )
         & (~Data['result_title'].str.contains(phrasedefault4_6_1e, na=False, case=False))
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
termlist4_6_2 = ["illitera", "analfabet", "analphabet", "innumeracy", "innumerate",
                 "analfabet", "lesekyn", "lesekunnig", "talkyn", "tallkyn", "talkunn", "talforståing", "tallforståelse"] 
                         
phrasedefault4_6_2 = r'\b(?:{})'.format('|'.join(termlist4_6_2))
```


```python
#Search 
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault4_6_2, na=False, case=False))   
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

```
TS=
(
  (
    ("educat*" OR "curricul*" OR "student assess*" OR "teaching" OR "teacher education" OR "teacher training" OR "online learning" OR "professional learning" 
     OR ("learn*" NEAR/5 "student*")
   )
  )
  NEAR/5
      ("sustainable development" OR "sustainable lifestyle$"
      OR "global citizen*" OR "glocal*"
      OR "human right*" OR "gender equality" OR "peace*" OR "non-violen*"
      OR "cultural divers*" OR "toleran*"
      OR
          ("sustainability"
          NEAR/5
              ("interdisciplinar*" OR "transdisciplinar*" OR "crossdisciplinar*" OR "cultural" OR "economic" OR "ecological"
              OR "participation" OR "agency" OR "responsibility"
              OR "ethic*" OR "wicked problem$" OR "complexity"
              OR "capacity for change" OR "transition$")
          )
  )
)


TS=
(
  ("education for sustainab*" OR "education in sustainab*" OR "education on sustainab*" OR "sustainable development education" OR "sustainability education"
    OR (("whole school" OR "teaching") NEAR/5 (("sustainab*" OR "ESD") NEAR/5 "educat*"))
   )
)

TS=
(
  (
    ("culture*" OR "cultural")
    NEAR/5 "sustainable development"
  )    
)


#### Phrase 1


```python
#Termlists
termlist4_7_1a = ["educat", "curricul", "student assess", "teaching", "teacher education", "teacher training", "online learning", "professional learning", 
                  "utdann", "opplæring", "pensum", "studieplan", "emneplan", "fagplan", "studentvurdering", "elevvurdering", "undervisning", "undervising", "nettbasert læring", "online læring", "profesjonslæring"
                 ]  
                  
termlist4_7_1b = ["learn",
                  "læring"
                 ]

termlist4_7_1c = ["vurdering"]

termlist4_7_1d =  ["student",
                   "elev"
                  ]  
                 
termlist4_7_1e = ["sustainable development", "sustainable lifestyle", "global citizen", "glocal", "human right", "gender equality", 
                  "peace", "non-violen", "cultural divers", "toleran",
                  "bærekraftig utvikling", "berekraftig utvikling", "berekraftig livsstil", "bærekraftig livsstil", 
                  "global borg", "globalt borg", "menneskerett", "likestilling", "ikkje-vald", "ikke-vold", "ikkevold", "ikkjevald", 
                  "kulturelt mangfold", "kulturelt mangfald"
                  ]
                  
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
    | 
        ((Data['result_title'].str.contains(phrasedefault4_7_1b, na=False, case=False))  
         &(Data['result_title'].str.contains(phrasedefault4_7_1d, na=False, case=False))
        )
    |  
        ((Data['result_title'].str.contains(phrasedefault4_7_1c, na=False, case=False)) 
         &(Data['result_title'].str.contains(phrasedefault4_7_1d, na=False, case=False))
        )
    )
    &
    (
     (Data['result_title'].str.contains(phrasedefault4_7_1e, na=False, case=False))
     | (Data['result_title'].str.contains(phrasespecific4_7_1i, na=False, case=False))
     | ((Data['result_title'].str.contains(phrasedefault4_7_1f, na=False, case=False)) 
        &(Data['result_title'].str.contains(phrasedefault4_7_1g, na=False, case=False))
       )
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
     & (
        (Data['result_title'].str.contains(phrasedefault4_7_2c, na=False, case=False)) 
        |(Data['result_title'].str.contains(phrasedespecific4_7_2c, na=False, case=True))  
       )
     & (Data['result_title'].str.contains(phrasedefault4_7_2d, na=False, case=False))
    )
),"tempsdg04_07"] = "SDG04_07"

print("Number of results = ", len(Data[(Data.tempsdg04_07 == "SDG04_07")])) 
```


```python
test=Data.loc[(Data.tempsdg04_07 == "SDG04_07"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

#### Phrase 3


```python
#Termlists
termlist4_7_3a = ["culture", "cultural",
                  "kultur"
                 ]
                                
termlist4_7_3b = ["sustainable development",
                  "bærekraft", "berekraft"
                  ]
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

```
TS=
(
 ("school*" OR "education facilit*")
  NEAR/5
    ("safe*" OR "secure*" OR "non-violen*" OR "inclus*" OR ("sensitive" NEAR/5 ("child*" OR "disability" OR "gender"))
  )
)


TS=
(
  (
    ("learning environment*" NEAR/5 "effective")
  )
  AND
    ("primary school*" OR "elementary school*" OR "primary educat*"
    OR "middle school*" OR "secondary school*" OR "secondary educat*"
    OR "school" OR "education" OR "learner*"
    )
)


TS=
(
 ("school*" OR "education* facility" OR "education* facilities") 
    NEAR/15  ("access*"
    NEAR/5
     ("electricity" OR "electrical supply" OR "modern energy" OR "internet" OR "computer*" OR "ICT facilit*" OR "adapted infrastructure*" OR "adapted material*" OR    "universal design" OR ("infrastructure" NEAR/5 "disab*") OR "drinking water" OR "sanitation" OR "handwash*" OR "hand wash*" OR "WASH facilities" OR "toilet$")
  )
) 
```


#### Phrase 1


```python
#Termlists
termlist4_a_1a = ["school", "education facilit",
                  "skole", "skule", "opplæring"
                  ]
                 
termlist4_a_1b = ["safe", "secure", "non-violen", "inclusive", 
                  "sikker", "sikre", "trygg", "barneven", "borneven", "ikke-vold", "ikkje-vald", "inkluder"
                  ]

termlist4_a_1c =  ["sensitiv",
                   "følsom", "hensyn", "omsyn"
                  ]

termlist4_a_1d = ["child", "disability", "gender",
                  "barn", "born", "funksjonshem", "funksjonsevne", "kjønn"
                  ]

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
        |
        (
            (Data['result_title'].str.contains(phrasedefault4_a_1c, na=False, case=False)) 
            &(Data['result_title'].str.contains(phrasedefault4_a_1d, na=False, case=False))
        )     
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
Here we have chosen a more simple search than in WoS. *Effective* is not included here, as this gave 0 hits.The structure here is then *Learning environment + School.*


```python
#Termlists
termlist4_a_2a = ["learning environment", 
                  "læringsmiljø"
                  ]
 
termlist4_a_2b =  ["primary school", "elementary school", "primary educat", "middle school", "secondary school", "secondary educat", "school", "education", "learner",
                    "skole", "skule", "utdann", "opplæring", "lærling"
                  ]

termlist4_a_2c = ["student", "universit", "higher education", "høyere utdanning", "høgare utdanning", "teacher education", "lærerutdanning", "lærarutdanning"]
                  
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
The structure from topic search in WoS is a bit simplified, as this returned 0 hits. *Access* is  not included, and the structure here is: *School + Basic services*


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

```
TS=
(
  (
    ("scholarships" OR "scholarship program*" OR "fellowship*" OR "sponsorship*" OR "exchange program*" OR "grant$")
    NEAR/15
        ("student*" OR "higher education" OR "trainee*" OR "student exchange$" OR "student mobility")
  )
AND
  (****LMICS****
  )
)





```python
#Termlists
termlist4_ba = ["scholarships", "scholarship program", "fellowship", "exchange program", 
                "student exchange", "student mobility", 

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
             (
                 (Data['result_title'].str.contains(phrasespecific4_bbuntrunc, na=False, case=False)) 
                 |(Data['result_title'].str.contains(phrasedefault4_bc, na=False, case=False)) 
             )
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

```
TS= 
  (
    ("teacher supply" OR  "supply of teacher$" OR "teacher coverage" 
    OR "teacher recruit*" OR "recruit* of teacher$" 
    OR "lack of teacher$" OR "teacher turnover" OR "teacher shortage" OR "teacher retention" OR "teacher attrition") 
  )

TS=
(
 ( 
  ("teacher training" OR "teacher education" OR "teacher qualification*" OR "qualifi* teacher$")
 )
  AND
    (****LMICs****
  )
)
```

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
        |
        (
            (Data['result_title'].str.contains(phrasespecific4_c_1b, na=False, case=False)) 
            &(Data['result_title'].str.contains(phrasedefault4_c_1c, na=False, case=False))
        )
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
        |
        (
            (Data['result_title'].str.contains(phrasedefault4_c_2b, na=False, case=False)) 
            & (Data['result_title'].str.contains(phrasedefault4_c_2c, na=False, case=False))
        )
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

```
TS=
("SDG 4" OR "SDGs 4" OR "SDG4" OR "sustainable development goal$ 4"
OR ("sustainable development goal$" AND "goal 4")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 4")
    AND ("quality education")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 4")
    NEAR/15 
        ("learning" OR "teaching" OR "teacher$" OR "early childhood" OR "child development" 
        OR "education for sustainable" OR "global citizenship education" OR "transdisciplinary education" OR "inclusive education" 
        OR "formal education" OR "primary education" OR "secondary education" OR "tertiary education" OR "higher education" OR "right$ to education" OR "access to education" OR "education for all" OR "education sector$"
        )
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  OR (("machine learning" OR "deep learning") NOT ("quality education" OR "SDG 4" OR "SDG4"))
  )
  ```
  
  Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 


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
      |
      (
        (Data['result_title'].str.contains(phrase_sdg4_b, na=False, case=False))
        & (Data['result_title'].str.contains(phrase_sdg4_c, na=False, case=False))
      )
      |
      (
         (Data['result_title'].str.contains(phrase_sdg4_d, na=False, case=False))
         & (Data['result_title'].str.contains(phrase_sdg4_e, na=False, case=False))
      )
      |
         (
           (Data['result_title'].str.contains(phrase_sdg4_e, na=False, case=False))
         & (Data['result_title'].str.contains(phrase_sdg4_f, na=False, case=False))
         )
      |(Data['result_title'].str.contains(phrase_sdg4_g, na=False, case=False))
),"tempmentionsdg04"] = "SDG04"
    
print("Number of results = ", len(Data[(Data.tempmentionsdg04 == "SDG04")])) 
```


```python
test=Data.loc[(Data.tempmentionsdg04 == "SDG04"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

## SDG 7

### SDG 7.1

*By 2030, ensure universal access to affordable, reliable and modern energy services*

*Innen 2030 sikre allmenn tilgang til pålitelige og moderne energitjenester til en overkommelig pris*

#### Phrase 1

```
TS=
(
  (
    ("energy transition$" NEAR/5 ("household$" OR "cooking" OR "stove$" OR "lighting" OR "lamps" OR "heating"))
    OR
      (
        ("clean*" OR "modern*")
        NEAR/5
            ("fuel$" OR "energ*" OR "electric*"
            OR "cooking" OR "stove$" OR "lighting" OR "lamps" OR "heating"
            )
      )
  )    
  AND ("household$" OR "homes" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic" OR "slum$" OR "village$" OR "women"
      )      
) 

```


```python
#Term lists
termlist7_1a = ["energy transition", 
                "energiomlegging", "energiomstilling"]
termlist7_1b = ["household", "cooking", "stove", "lighting", "lamps", "heating",
                "hushold", "hushald", "matlaging", "komfyr", "ovn", "lys", "lampe", "oppvarming"]
termlist7_1c = ["clean fuel", "clean energy", "clean electricity", "clean cooking", "clean stove", "clean lighting", "clean lamp", "clean heating",
                "modern fuel", "modern stove", "modern lighting", "modern lamps", "modern heating",
                "rent brennstoff", "reint brennstoff", "rentbrennende", "reintbrennande", "ren energi", "rein energi", "ren strøm", "rein straum", "ren elektrisitet", "rein elektrisitet"
               ]
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

```
TS=
(
  "solar cooker$" OR "solar box cooker$" OR "solar cooking"
  OR "improved cookstove$" OR "improved stove$" OR "modern cookstove$" OR "modern stove$"
)
```


```python
#Term lists
termlist7_1e = ["solar cook", "solar box cook", "improved cookstove", "improved stove", "modern cookstove", "modern stove"
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

```
TS=
(
  ("kerosene" OR "solid fuel$" OR "coal"
  )    
  NEAR/15
      ("household$" OR "homes" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic use*" OR "slum" OR "slums" OR "women"
      OR "residential heating" OR "central heating" OR "winter heating" OR "cooking" OR "stove$" OR "lighting" OR "lamps"
      )      
)
OR
TS=
(
  ("coal")    
  NEAR/15
      ("household$" OR "homes" OR "house" OR "houses" OR "housing"
      OR "residential" OR "dwelling$" OR "domestic use*" OR "slum" OR "slums" OR "women"
      OR "heating" OR "cooking" OR "stove$" OR "lighting" OR "lamps"
      )      
)
```


```python
#Term lists
termlist7_1f = ["kerosene", "solid fuel.*", "coal"
              "parafin.*", "fast bren.*", "koks"] 
termlist7_1g = ["household", "home", "hous", "residential", "dwelling", "domestic use", "slum", "women", "residential heating", "central heating", "winter heating",
                "heating", "cooking", "stove", "lighting", "lamps",
                
                "hushold", "hushald", "hjem", "heim", "hus", "bolig", "bustad", "slum", "kvinne", 
                "oppvarming", "varme", "fyre", "fyring", "matlaging", "ovn", "lys", "belysning", "ljos", "lampe"]     
                #There is no Norwegian translation of the search term "coal" as it only returns noise, not really a common fuel in Norway         

phrasespecific7_1f = r'\b(?:{})\b'.format('|'.join(termlist7_1f))
phrasedefault7_1g = r'(?:{})'.format('|'.join(termlist7_1g))
```


```python
#Search 7_1fg
Data.loc[(
    (Data['result_title'].str.contains(phrasespecific7_1f, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault7_1g, na=False, case=False)) 
),"tempsdg07_01"] = "SDG07_01"

print("Number of results = ", len(Data[(Data.tempsdg07_01 == "SDG07_01")])) 
```


```python
test=Data.loc[(Data.tempsdg07_01 == "SDG07_01"), ("result_id", "result_title")]
test.iloc[0:8, ]
```

#### Phrase 4


```
TS=
(
  "energy poverty" OR "energy vulnerability" OR "fuel poverty"
  OR "energy democracy" OR "energy justice" OR "energy inequity"
  OR "energy security" OR "energy insecurity"
)
```


```python
#Term lists
termlist7_1h = ["energy poverty", "energy vulnerability", "fuel poverty", "energy democracy", "energy justice", "energy inequity", "energy security", "energy insecurity" 
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


```
TS= ("universal electrification" OR "rural electrification" OR "national electrification")
OR
TS=
(
  ("access" OR "provision")
  NEAR/5
      ("energy service$" OR "electricity supply"
      OR
        (
          ("energy" OR "power" OR "electric*")
          NEAR/3
              ("household$" OR "home$" OR "house" OR "houses" OR "housing"
              OR "residential" OR "dwelling$" OR "domestic use*" OR "slum$" OR "village$"
              OR "sustainable" OR "green" OR "clean" OR "modern"
              )            
        )
      )
)
OR
TS=
(
  ("electrification" OR "grid extension$"
  OR
    (
      ("access" OR "provision")
      NEAR/5 ("energy" OR "electricity" OR "electrical supply" OR "power supply")
    )
  )
  NEAR/15
      ("rural"
      OR ("remote" NEAR/3 ("region$" OR "area" OR "areas" OR "communities" OR "community"))
      OR ****LMICs****
      )
)
```




```python
#Term lists - 
termlist7_1i = ["electricity", "energy", "power", "universal electrification", "rural electrification", "national electrification", "electrification", "grid extension", "grid extensions",
                "access to energy", "provision of energy", "energy provision", "provision of electricity", "electricity provision", "electricity supply", "electrical supply", "power supply",
                "elektrisitet", "strøm", "straum", "energi", "kraft", "elektrifisering", "elektrisering", "mikronett", "øydrift", "tilgang til energi", "tilgang på energi", "energitilgang",
                "tilgang til elektrisitet", "tilgang på elektrisitet", "tilgang til strøm", "tilgang til straum", "tilgang på strøm", "tilgang på straum"]
termlist7_1j = ["household", "home", "house", "housing", "residential", "dwelling", "domestic use", "slum", "village","sustainable", "green", "clean","modern",
                "hushold", "hushald", "hjem", "heim", "hus", "bolig", "bustad", "slum", "landsby","bærekraftig", "berekraftig", "grøn", "ren", "rein", "moderne"]
termlist7_1k = ["rural", "remote region", "remote area", "remote communit", 
                "landlig", "landsby",
                ] 
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
            |
            (
                (Data['result_title'].str.contains(phrasedefault7_1xtr, na=False, case=False))
                &(Data['result_title'].str.contains(phrasedefault7_1j, na=False, case=False))  
            )
        )
    )
    |
    (
        (
            (Data['result_title'].str.contains(phrasedefault7_1xtra, na=False, case=False))
            | ((Data['result_title'].str.contains(phrasedefault7_1x, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault7_1xtras, na=False, case=False)))
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

```
TS= 
(
  ("stable" OR "stability" OR "reliab*" OR "resilien*" OR "afford*" OR "inexpensive" OR "low cost" OR "cheap"
  OR "unstable" OR "instability" OR "unreliab*" OR "unafford*" OR "costly" OR "energy cost$" OR "expensive"
  )
  NEAR/15
      ("energy service$" OR "electricity supply"
      OR
        (
          ("energy" OR "power" OR "electric*")
          NEAR/5
              ("household$" OR "home$" OR "house" OR "houses" OR "housing"
              OR "residential" OR "dwelling$" OR "domestic use*" OR "slum" OR "slums" OR "village$"
              OR "sustainable"
              )            
        )
      OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$"
      OR "off grid solution$" OR "off-grid system$"
      OR (("energy" OR "electricity") NEAR/3 ("infrastructure" OR "off grid" OR "decentrali$ed" OR "cooperative$"))
      OR "community energy" OR "community renewable energy"
      )
)      

```




```python
#Term lists
termlist7_1l = ["stable", "stability", "reliable", "reliability" "resilient", "resilience", "affordable", "affordability", "inexpensive", "low cost", "cheap", 
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
        |(
            (Data['result_title'].str.contains(phrasedefault7_1n, na=False, case=False)) 
            &(Data['result_title'].str.contains(phrasedefault7_1o, na=False, case=False))
        )
        |(Data['result_title'].str.contains(phrasedefault7_1p, na=False, case=False)) 
        |(
            (Data['result_title'].str.contains(phrasedefault7_1q, na=False, case=False)) 
            &(Data['result_title'].str.contains(phrasedefault7_1r, na=False, case=False)) 
        )
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

```
TS=
(
  ("renewable" AND ("energy transition$" OR "sector transformation$" OR "energy transformation$"))
  OR ("renewable energy" NEAR/15 ("substitut*" OR "uptake"))
)



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
  (
    (Data['result_title'].str.contains(phrasedefault7_2a, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault7_2b, na=False, case=False)) 
  )
 |
  (
    (Data['result_title'].str.contains(phrasedefault7_2c, na=False, case=False)) 
    & (Data['result_title'].str.contains(phrasedefault7_2d, na=False, case=False)) 
  )   
),"tempsdg07_02"] = "SDG07_02"

print("Number of results = ", len(Data[(Data.tempsdg07_02 == "SDG07_02")])) 
```


```python
test=Data.loc[(Data.tempsdg07_02 == "SDG07_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```
TS=
(
  ("relian*" OR "primary use" OR "primary usage" OR "primary source$" OR "adopting" OR "adoption" OR "implementation" OR "uptake" 
  OR "contribution" OR "proportion" OR "share" OR "expansion"
  OR "feasibility" OR "attractiveness" OR "incentive$" OR "initiative$"
  OR "affordab*" OR "inexpensive" OR "low cost" OR "economic feasibility" OR "economic viability" OR "cost-effectiveness" OR "cost-advantage$"
  OR "investment$" OR "subsidies" OR "subsidi$ation" OR "financing" OR "funding" OR "commerciali?ation"
  OR "energy service$" OR "energy sector" OR "generation" OR "capacity"
  OR "global energy" OR "global electricity" OR "energy mix" OR "market share$"
  OR "barrier$" OR "obstacle$"
  OR "implement" OR "adopt" OR "incentivi*"
  OR "energy transition$" OR "renewable transition$" OR "transition* to"
  OR ("certificat*" NEAR/2 ("energy" OR "green"))
  OR "policy" OR "policies" OR "legislation" OR "kyoto protocol" OR "strateg*" OR "energy management" OR "energy planning"
  OR "subsidi$e" OR "investing" OR "invest" OR "green bond$" OR "climate bond$" OR "feed-in tariff$"
  OR "upscale" OR "scale-up" OR "commercial development" OR "develop* commercially" OR "roll out" OR "rollout"
  OR "sustainable development" OR "sustainable energy development"
  )
  NEAR/15
      ("non conventional energy"
      OR
        (
          ("electricity" OR "power" OR "powered" OR "energy")
          NEAR/5
              ("renewable$"  OR "sustainable" OR "green"
              OR "hydrothermal" OR "geothermal"
              OR "hydroelectric" OR "hydropower" OR "hydro"
              OR "hydrokinetic"
              )    
        )
      OR "geothermal heat pump$" OR "ground source heat pump$"
      OR "solar cell$" OR "solar-cell$" OR "solar panel$" OR "solar-panel$" OR "solar power*" OR "solar array" OR "solar PV" OR "solar photovoltaic$"
      OR "solar energy collector$" OR "solar farm$" OR "solar plant$" OR "solar park$"
      OR "solar district heating" OR "solar district cooling" OR "solar air heating system$" OR "solar space heating system$"
      OR ("solar thermal" NEAR/3 ("power" OR "technolog*" OR "collector$" OR "district"))
      OR ("solar thermal energy" NEAR/15 ("power" OR "electric*" OR "water heating" OR "industrial process heat*"))
      OR "wind farm$" OR "wind turbine$" OR "wind park$" OR "wind factory" OR "wind factories"
      OR "tidal turbine$" OR "stream turbine$" OR "current turbine$"
      OR "tidal power" OR "tidal energy" OR "marine energy"
      OR ("wave energy" NEAR/5 ("converter$" OR "renewable" OR "power" OR "generat*" OR "energy harvesting"))
      OR "biofuel$" OR "bioenergy" OR "biodiesel"
      OR
        (
          ("biomass" OR "wind" OR "solar" OR "ammonia")
          NEAR/10
              ("electric*" OR "energy generat*" OR "energy service$" OR "energy sector"
              OR "energy system$" OR "power system$"
              OR "energy crop$" OR "energy security"
              )
        )
      OR ("hydrogen" NEAR/10 ("renewable substitute$" OR "renewable source$" OR "green"))
      OR
        (
          ("fuel cell$" OR "battery" OR "batteries" OR "lithium ion" OR "energy storage" OR "smart grid$")
          NEAR/15 ("renewable" OR "sustainab*")
        )
      )
)
```



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
                "solar photovoltaic", "solar energy collector", "solar farm", "solar plant", "solar park", "solar district heating", "solar district cooling", 
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
   (
      (Data['result_title'].str.contains(phrasedefault7_2c, na=False, case=False))|
      (Data['result_title'].str.contains(phrasespecific7_2c, na=False, case=False))
   ) 
   &
    (
        (Data['result_title'].str.contains(phrasedefault7_2d, na=False, case=False))
 | 
    (
      (Data['result_title'].str.contains(phrasespecific7_2e, na=False, case=False))
      &
      (Data['result_title'].str.contains(phrasedefault7_2f, na=False, case=False))
    )
    
  |
    (Data['result_title'].str.contains(phrasedefault7_2g, na=False, case=False))
  |
     (
       (Data['result_title'].str.contains(phrasedefault7_2h, na=False, case=False))& 
       (Data['result_title'].str.contains(phrasedefault7_2i, na=False, case=False))  
     )
  |
    (
      (Data['result_title'].str.contains(phrasedefault7_2j, na=False, case=False))&
      (Data['result_title'].str.contains(phrasedefault7_2k, na=False, case=False))
    )   
  |
      
    (
       (
          (Data['result_title'].str.contains(phrasedefault7_2l, na=False, case=False))|
          (Data['result_title'].str.contains(phrasedefault7_2m, na=False, case=False))
      )
        &
       (Data['result_title'].str.contains(phrasedefault7_2n, na=False, case=False))
    )
   |
      (Data['result_title'].str.contains(phrasedefault7_2o, na=False, case=False)) 
   |
    (
        (Data['result_title'].str.contains(phrasedefault7_2p, na=False, case=False))&
        (Data['result_title'].str.contains(phrasedefault7_2q, na=False, case=False))
    )  
  |
    (
        (Data['result_title'].str.contains(phrasedefault7_2r, na=False, case=False))&
        (Data['result_title'].str.contains(phrasedefault7_2s, na=False, case=False))
    )   
  |
    (
        (Data['result_title'].str.contains(phrasedefault7_2t, na=False, case=False))&
        (Data['result_title'].str.contains(phrasedefault7_2u, na=False, case=False))
    )  
)
),"tempsdg07_02"] = "SDG07_02"

print("Number of results = ", len(Data[(Data.tempsdg07_02 == "SDG07_02")]))  
```


```python
test=Data.loc[(Data.tempsdg07_02 == "SDG07_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3

The Web of Science search proved very restricive, and a direct translation of it did not return many hits in the title search. Therefore we added "coal" and allowed "energy" to stand alone (as opposed to the WoS search where it is used in phrases like "energy service", "energy supply" etc). This results in some noise, but also returns considerable more relevant hits. 

```
TS=
(
  ("fossil fuel$" OR "coal" OR "natural gas" OR "grey hydrogen" OR "conventional energy"
  OR
    (
      ("reduce" OR "decreas*" OR "phase out" OR "phasing out"
      OR "improv*" OR "incentiv*" OR "support" OR "encourag*"
      OR "transition*" OR "substitut*" OR "intervention$"
      OR "policy" OR "policies" OR "legislation" OR "energy strateg*" OR "energy management" OR "energy planning"
      )
      NEAR/5
          ("oil")
    )
  )
  NEAR/15
    ("relian*" OR "primary use" OR "primary usage" OR "primary source$"
    OR "coal consumption" OR "fossil fuel consumption" OR "consumption of fossil fuel$"
    OR "energy service$" OR "energy sector" OR "energy supply" OR "energy supplies"
    OR "global energy" OR "global electricity" OR "energy mix"
    )
)   
```


```python
# Term lists
termlist7_2m = ["fossil fuel", "natural gas", "grey hydrogen", "conventional energy", 
                "fossilt brensel", "fossile brensl", "fossilt brennstoff", "fossile brennstoff", "naturgass", "grått hydrogen", "konvensjonell energi"]
termlist7_2mtrunk = ["coal", 
                     "kull", "kol"]
termlist7_2n = ["reduc", "decreas", "phase out", "phasing out", "improv", "incentiv", "support", "encourag", "transition", "substitut", 
                "intervention", "policy", "policies", "legislation", 
                "energy strateg", "energy management", "energy plan"
                "reduser", "reduksjon", "mink", "utfas", "fase ut", "bedre", "betr", "insentiv", "støtte", "stønad", "oppmuntr", "oppmod", "omstill",
                "erstat", "intervensjon", "inngrip", "politikk", "retningslin", "lovgiv", "energistrategi", "energiledelse", "energileiing", "energiplan"]
termlist7_2o = ["olje"]
termlist7_2otrunk = ["oil", "coal", 
                     "kull", "kol"]
termlist7_2p = ["relian", "primary use", "primary usage", "primary source", "consumption", "consumption of fossil fuel", "global electricity", "energy",
                "avhengig", "primær bruk", "primærbruk", "primær kilde", "primær kjelde", "primærkilde", "primærkjelde", "forbruk", "global elektrisitet", "energi"]
                                                
phrasedefault7_2m = r'(?:{})'.format('|'.join(termlist7_2m))
phrasespecific7_2mtrunk = r'\b(?:{})\b'.format('|'.join(termlist7_2mtrunk))
phrasedefault7_2n = r'(?:{})'.format('|'.join(termlist7_2n))
phrasedefault7_2o = r'(?:{})'.format('|'.join(termlist7_2o))
phrasespecific7_2otrunk = r'\b(?:{})\b'.format('|'.join(termlist7_2otrunk))
phrasedefault7_2p = r'(?:{})'.format('|'.join(termlist7_2p))
```


```python
#Search 7_2mnop
Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault7_2m, na=False, case=False))
            |(Data['result_title'].str.contains(phrasespecific7_2mtrunk, na=False, case=False))
        )
        |  
        (
            (Data['result_title'].str.contains(phrasedefault7_2n, na=False, case=False))     
            & 
            (
                (Data['result_title'].str.contains(phrasedefault7_2o, na=False, case=False))
                |(Data['result_title'].str.contains(phrasespecific7_2otrunk, na=False, case=False))
            )
        )
    )
    & (Data['result_title'].str.contains(phrasedefault7_2p, na=False, case=False))
),"tempsdg07_02"] = "SDG07_02"

print("Number of results = ", len(Data[(Data.tempsdg07_02 == "SDG07_02")]))  
```


```python
test=Data.loc[(Data.tempsdg07_02 == "SDG07_02"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

### SDG 7.3

*By 2030, double the global rate of improvement in energy efficiency*

*Innen 2030 få forbedringen av energieffektivitet på verdensbasis til å gå dobbelt så fort*

#### Phrase 1

```
TS=
(
  ("energy intensity")
  AND
      ("energy consum*" OR "sustainab*" OR "energy efficiency"
      OR "GDP" OR "economic" OR "economy" OR "economies"
      OR "industry" OR "industrial" OR "manufacturing"
      OR ("emission$" NEAR/5 ("carbon" OR "co2"))
      OR "footprint$"
      )
)
```


```python
# Term lists
termlist7_3a = ["energy intensity", 
                "energiintensitet" ]
#termlist7_3b = ["energy consum", "sustainab", "energy efficiency", "GDP", "economic", "economy", "economies", "industr", "manufacturing", "footprint",
#                "energiforbruk", "bærekraft", "berekraft", "BNP", "økonomi", "industri", "produksjon", "fotavtrykk"]
#termlist7_3c = ["emission",
#                "utslipp", "utslepp"]
#termlist7_3d = ["carbon", "co2", 
#                "karbon"]
# As "energy intensity" is such a specialized term, we found it sufficient to search for it alone in the title search.

phrasedefault7_3a = r'(?:{})'.format('|'.join(termlist7_3a))
#phrasedefault7_3b = r'(?:{})'.format('|'.join(termlist7_3b))
#phrasedefault7_3c = r'(?:{})'.format('|'.join(termlist7_3c))
#phrasedefault7_3d = r'(?:{})'.format('|'.join(termlist7_3d))
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

```
TS=
(
  ("energy consum*"
  NEAR/5 ("decoupl*" OR "de coupl*")
  )
  NEAR/5 ("econom*" OR "GDP")
)
``` 



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
    &(Data['result_title'].str.contains(phrasedefault7_3g, na=False, case=False))
),"tempsdg07_03"] = "SDG07_03"

print("Number of results = ", len(Data[(Data.tempsdg07_03 == "SDG07_03")]))  
```


```python
test=Data.loc[(Data.tempsdg07_03 == "SDG07_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3

```
TS=
(
    (
      ("energy efficien*" OR "energy utili$ation efficiency" OR "energy saving" OR "energy loss" OR "energy conservation")
      NEAR/15
          ("housing" OR "houses" OR "homes" OR "household" OR "domestic" OR "residential" OR "building$" OR "cities"
          OR "service sector" OR "office$" OR "retail" OR "food services" OR "restaurants" OR "hotels" OR "warehouses"
          OR "lighting" OR "lamps" OR "cooking" OR "appliances" OR "white goods"
          OR "plug-in device$" OR "smart"
          OR "space cooler$" OR "air condition*" OR "space heat*" OR "room heating" OR "district heating" OR "heat pump$" OR "HVAC"
          OR "industry" OR "industrial" OR "manufacturing" OR "technolog*"
          OR "transport" OR "transportation" OR "vehicles" OR "cars" OR "train$" OR "airplane$" OR "aeroplane$" OR "ship$" OR "shipping" OR "freight"
          OR "telecomm*" OR "data centre$" OR "data center$" OR "data network$" OR "server" OR "servers" OR "wireless"
          )
    )
    OR
      (("energy efficiency" OR "energy conservation")
      NEAR/5
            ("policy" OR "policies" OR "framework$" OR "legislation" OR "management" OR "planning" OR "plan" OR "plans"
            OR "initiative$" OR "intervention$" OR "incentive$" OR "investment$" OR "investing" OR "invest"
            )
      )
    OR
      ("energy efficiency"
      NEAR/15
            ("green bond$" OR "climate bond$"
            OR ("certificat*" NEAR/2 ("energy" OR "green"))
            OR "energy sustainability"
            OR "minimum energy performance" OR "energy labelling" OR "energy standard$" OR "energy efficiency standard$"
            OR "sustainable development"
            )
      )
)
```



```python
# Term lists

# A direct translation of the Web of Science search into Norwegian language gave barely any results. 
# We therefore allowed a few terms for energy efficiency and energy saving in Norwegian to stand alone in order to capture some more relevant titles (list 3no below). 
# This was not done in english because it produces noise.
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
termlist7_3no = ["energieffektiv", "energispar", "energiøkonomiser"]

phrasedefault7_3h = r'(?:{})'.format('|'.join(termlist7_3h))
phrasedefault7_3i = r'(?:{})'.format('|'.join(termlist7_3i))
phrasedefault7_3j = r'(?:{})'.format('|'.join(termlist7_3j))  
phrasedefault7_3k = r'(?:{})'.format('|'.join(termlist7_3k))
phrasedefault7_3l = r'(?:{})'.format('|'.join(termlist7_3l))
phrasedefault7_3m = r'(?:{})'.format('|'.join(termlist7_3m))              
phrasedefault7_3no = r'(?:{})'.format('|'.join(termlist7_3no))
```


```python
## Search 7_3hijklmno 
Data.loc[(
  (
      (
          (Data['result_title'].str.contains(phrasedefault7_3h, na=False, case=False))
          &(Data['result_title'].str.contains(phrasedefault7_3i, na=False, case=False))
      )
      |
      (
          (Data['result_title'].str.contains(phrasedefault7_3j, na=False, case=False))
          &(Data['result_title'].str.contains(phrasedefault7_3k, na=False, case=False))
      )
      |
      (
          (Data['result_title'].str.contains(phrasedefault7_3l, na=False, case=False))
          &(Data['result_title'].str.contains(phrasedefault7_3m, na=False, case=False))
      )
  )
  | (Data['result_title'].str.contains(phrasedefault7_3no, na=False, case=False))
),"tempsdg07_03"] = "SDG07_03"

print("Number of results = ", len(Data[(Data.tempsdg07_03 == "SDG07_03")])) 
```


```python
test=Data.loc[(Data.tempsdg07_03 == "SDG07_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 4
We have simplified the search as we are only searching titles, and left out many specific energy terms. All that is required now is terms for "energy efficien" or "sufficien" to be combined with "energy sufficiency".

```
TS=
  ("energy sufficiency"
  AND
      ("electric*" OR "energy generat*" OR "energy service$" OR "energy sector" OR "energy system$"
      OR "power system$" OR "energy security" OR "renewable energy"
      )
  )
```



```python
# Term lists
termlist7_3n = ["energy sufficiency"]
termlist7_3o = ["electric", "energy generat", "energy service", "energy sector", "energy system", "power system", "energy security", "renewable energy"]
termlist7_3p = ["energy",
                "energi"]
termlist7_3q = ["sufficien", "suffisien", 
                "tilstrekkelig"]
termlist7_3r = ["energy efficien", 
                "energieffektiv"]

phrasedefault7_3n = r'(?:{})'.format('|'.join(termlist7_3n))
phrasedefault7_3o = r'(?:{})'.format('|'.join(termlist7_3o))
phrasedefault7_3p = r'(?:{})'.format('|'.join(termlist7_3p))
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

```
TS=
(
  ("ODA" OR "development spending" OR "cooperation fund"
  OR  
    (
      ("international" OR "development" OR "foreign")
      NEAR/3
          ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
          OR "aid" OR "assistance"
          OR "fund$" OR "grant$" OR "financing" OR "financial resources" OR "capital flow$"
          )
    )
  OR  
    (
      ("knowledge" OR "technolog*" OR "technical" OR "research" OR "scientific" OR "R&D")
      NEAR/5 ("access*" OR "capacity" OR "transfer" OR "sharing" OR "shared" OR "share" OR "cooperat*" OR "co-operat*" OR "collaborat*" OR "partnership$")
    )
  OR "invest" OR "investing" OR "investment$" OR "financing" OR "funding" OR "financial resources"
  OR (("financial*" or "monetary") NEAR/3 ("support*" or "assist*"))
  OR "economic support" OR "economic assistance"
  OR "green bond$" OR "climate bond$"
  )
  NEAR/15
      ("cleantech" OR "energy research" OR "energy efficiency research" OR "energy transition$" OR "energy technolog*"
      OR
        (
          ("technolog*" OR "innovation$" OR "R&D")
          NEAR/3
              ("clean" OR "cleaner" OR "green" OR "greener"
              OR "decarboni*" OR "low carbon" OR "energy efficien*"  
              OR "renewable$" OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower" OR "marine energy" OR "tidal energy" OR "wave energy"
              )
        )      
      )             
)
```



```python
# Term lists
termlist7_a1 = ["ODA", "development spending", "cooperation fund", 
                "bistand", "utviklingshjelp", "u-hjelp", "samarbeidsfond"]
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
termlist7_a9 = ["cleantech", "energy research", "energy efficiency research", "energy transition", "energy technolog",
                "ren teknologi", "rein teknologi", "energiforskning", "energiforsking", "energiomstilling", "energiteknologi"] 
termlist7_a10 = ["technolog", "innovation", "R&D",
                 "teknologi", "innovasjon", "FOU"]
termlist7_a11 = ["clean", "green", "decarboni", "low carbon", "energy efficien", "renewable", "solar", "wind", "geothermal", "hydroelectric", 
                 "hydro electric", "hydro power", "marine energy", "tidal energy", "wave energy",
                 "rein", "avkarboniser", "lavkarbon", "lågkarbon", "energieffektiv", "fornybar", "solcelle", "solkraft", "solenergi", "solcelle", 
                 "solkraft", "solenergi", "vind", "geotermisk", 
                 "hydroelektrisk", "vannkraft", "vasskraft", "havenergi", "tidevannsenergi", "tidvass", "bølgeenergi"]      

phrasedefault7_a1 = r'(?:{})'.format('|'.join(termlist7_a1))
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
  |
    (
      (Data['result_title'].str.contains(phrasedefault7_a2, na=False, case=False))&
      (Data['result_title'].str.contains(phrasedefault7_a3, na=False, case=False))
    )
  |
    (
      (Data['result_title'].str.contains(phrasedefault7_a4, na=False, case=False))&
      (Data['result_title'].str.contains(phrasedefault7_a5, na=False, case=False))
    )
  |
    (Data['result_title'].str.contains(phrasedefault7_a6, na=False, case=False))
  |
    (
      (Data['result_title'].str.contains(phrasedefault7_a7, na=False, case=False))& 
      (Data['result_title'].str.contains(phrasedefault7_a8, na=False, case=False))
    )
 )
 &
  (
      (Data['result_title'].str.contains(phrasedefault7_a9, na=False, case=False))
  |
    (
       (Data['result_title'].str.contains(phrasedefault7_a10, na=False, case=False))&
       (Data['result_title'].str.contains(phrasedefault7_a11, na=False, case=False))
    )
  ) 
),"tempsdg07_a"] = "SDG07_0a"

print("Number of results = ", len(Data[(Data.tempsdg07_a == "SDG07_0a")]))  
```


```python
test=Data.loc[(Data.tempsdg07_a == "SDG07_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2

```
TS=
(
  ("ODA" OR "development spending" OR "cooperation fund"
  OR  (
        ("international" OR "development" OR "foreign")
        NEAR/3
            ("cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
            OR "aid" OR "assistance"
            OR "fund$" OR "grant$" OR "financing" OR "financial resources" OR "capital flow$"
            )
      )
  OR "invest" OR "investing" OR "investment$" OR "financing" OR "funding" OR "financial resources"
  OR (("financial*" or "monetary" OR "economic") NEAR/3 ("support*" or "assist*" OR "resources"))
  OR "green bond$" OR "climate bond$"  
  )
  NEAR/15
      ("energy service$" OR "energy sector" OR "electrical infrastructure" OR "electricity supply" OR "power supply"
      OR (("energy" OR "electricity") NEAR/5 ("infrastructure" OR "technolog*" OR "off grid" OR "decentrali$ed" OR "cooperative$"))
      OR "community energy" OR "community renewable energy"
      OR "electrical grid$" OR "power grid$" OR "grid extension$" OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$" OR "smart grid$" OR "energy storage system$"
      OR "energy transition$"
      OR
        (
          ("power station$" OR "power generation" OR "energy generation" OR "generator$")
          NEAR/5
              ("modern" OR "clean" OR "sustainable" OR "renewable$" OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower" OR "marine" OR "tidal" OR "wave energy")
        )             
      )            
)
```



```python
# Term lists
termlist7_a12 = ["ODA", "development spending", "cooperation fund", 
                 "offisiell utviklingsbistand", "offentlig utviklingsbistand", "bistand", "utviklingshjelp", "u-hjelp", "samarbeidsfond"]
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
termlist7_a18 = ["energy service", "energy sector", "electrical infrastructure", "electricity supply", "power supply", "community energy", 
                 "community renewable energy", "electrical grid", "power grid", "grid extension", "microgrid", "micro grid", "micro-grid", 
                 "minigrid", "mini grid", "mini-grid", "smartgrid", "smart grid", "smart-grid", "energy storage system", "energy transition",
                 
                 "energitjeneste", "energiteneste", "energisektor", "energiinfrastruktur", "elektrisk infrastruktur", "energiforsyning",
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
                 "bærekraftig", "berekraftig", "fornybar", "sol", "vind", "geotermisk", "hydroelektrisk", "vannkraft", "vasskraft", 
                 "hav", "tidevann", "tidvass", "bølgeenergi"]                                        

phrasedefault7_a12 = r'(?:{})'.format('|'.join(termlist7_a12))
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
        |
        (
            (Data['result_title'].str.contains(phrasedefault7_a13, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault7_a14, na=False, case=False))
        )
        |(Data['result_title'].str.contains(phrasedefault7_a15, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasedefault7_a16, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault7_a17, na=False, case=False))
        )  
    ) 
    &
    (
        (Data['result_title'].str.contains(phrasedefault7_a18, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasedefault7_a19, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault7_a20, na=False, case=False))
        )
        |
        (
            (Data['result_title'].str.contains(phrasedefault7_a21, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault7_a22, na=False, case=False)) 
        )
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

```
TS=
(
  (
    ("modern*" OR "clean" OR "sustainable" OR "renewable$" OR "decarboni*" OR "low carbon"
    OR "improv*" OR "increas*" OR "strengthen*" OR "enhanc*" OR "better"
    OR "more efficient" OR "upgrad*" OR "scal* up"
    OR "build" OR "expand*" OR "extend*" OR "deploy" OR "accelerat*" OR "prioriti$e"
    OR "energy sector transform*"
    )  
    NEAR/5  
      ("energy service$" OR "energy sector" OR "electrical infrastructure" OR "electricity supply" OR "power supply"
      OR (("energy" OR "electricity") NEAR/5 ("infrastructure" OR "technolog*" OR "off grid" OR "decentrali$ed" OR "community" OR "cooperative$"))
      OR "electrical grid$" OR "power grid$" OR "grid extension$" OR "microgrid$" OR "micro grid$" OR "minigrid$" OR "mini grid$" OR "smart grid$" OR "energy storage system$"
      OR
        (
          ("power station$" OR "power generation" OR "energy generation" OR "generator$")
          NEAR/5
              ("modern*" OR "clean" OR "sustainable" OR "renewable$" OR "decarboni*" OR "low carbon"
              OR "solar" OR "wind" OR "geothermal" OR "hydroelectric" OR "hydro electric" OR "hydropower" OR "marine" OR "tidal" OR "wave energy"
              )
        )             
      )
  )
  AND  
    (****LMICSs****
    )
)
```
      


```python
# Term lists
termlist7_b1 = ["energy service", "energy sector", "electrical infrastructure", "electricity supply", "power supply", "energy", "electricity",
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
        ( 
            (Data['result_title'].str.contains(phrasedefault7_b1, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault7_b2, na=False, case=False))
        )
        |
        (
            (Data['result_title'].str.contains(phrasedefault7_b3, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault7_b4, na=False, case=False))
        )
    ) 
    & (Data['LMICs']==True)
),"tempsdg07_b"] = "SDG07_b"
```


```python
print("Number of results = ", len(Data[(Data.tempsdg07_b == "SDG07_b")])) 
```

### SDG 7 mentions


```
TS=
("SDG 7" OR "SDGs 7" OR "SDG7" OR "sustainable development goal$ 7"
OR ("sustainable development goal$" AND "goal 7")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 7")
    AND ("clean energy")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 7")
    NEAR/15 ("energy")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
  ```
  
  Here it was not neccesary to exclude the NOT terms used in a normal abstract search, so they are not used. But in other contexts/abstract searches it may be necessary to add them in again. 


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
      |
        (
          (Data['result_title'].str.contains(phrasedefault7_2, na=False, case=False))&
          (Data['result_title'].str.contains(phrasedefault7_3, na=False, case=False))
        ) 
      |
        (
         (Data['result_title'].str.contains(phrasedefault7_4, na=False, case=False))&
         (Data['result_title'].str.contains(phrasedefault7_5, na=False, case=False))
        )
      |
        (Data['result_title'].str.contains(phrasedefault7_6, na=False, case=False))
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
```
TS=
(
  ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*" OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*"
  )
  NEAR/15
      (
        ("adequa*" OR "inadequa*" OR "affordab*" OR "afford" OR "low cost" OR "inexpensive"
        OR "safe" OR "unsafe" OR "safety" OR "secure" OR "insecure" OR "security"
        OR "tenure"
        )
        NEAR/5 ("housing" OR "settlements" OR "living conditions")
      )
)
```


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
```
TS=
(
  (
    ("access" OR "obstacle" OR "barrier" OR "hinder*" OR "hindrance*" OR "equitab*" OR "non-equit*" OR "legislat*" OR "govern*" OR "strateg*" OR "policy" OR "policies" OR "framework$" OR "program*"
    )
    NEAR/15
        (
          ("basic" NEAR/2 ("service$" OR "facility" OR "facilities"))
          OR
            (
              ("drinking water" OR "sanitation" OR "hygiene" OR "toilet" OR "handwashing" OR "hand-washing" OR "sewage" OR "WASH")
	            NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "safe")
            )
          OR "improved drinking water" OR "improved source$ of drinking water" OR "clean drinking water" OR "clean water"
          OR (("waste" OR "garbage" OR "rubbish") NEAR/2 ("service$" OR "facility" OR "facilities"))
          OR (("health" OR "medical") NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "essential" OR "primary" OR "care"))
          OR "healthcare"
          OR (("education*" OR "school*") NEAR/2 ("service$" OR "facility" OR "facilities" OR "basic" OR "primary"))
          OR
            (
              ("basic information" OR "telecommunication" OR "basic communication" OR "ICT")
	            NEAR/2 ("service$" OR "facility" OR "facilities" OR "infrastructure")
            )
          OR "electricity service$" OR "energy service$" OR "modern energy" OR "clean fuel$" OR "clean energy"
          OR "public open space$" OR "public space$"
          OR "basic mobility" OR "urban mobility" OR "rural mobility" OR "all-season road$"
          OR ("transport*" NEAR/2 ("service$" OR "infrastructure" OR "system$" OR "public"))
        )
  )
  NEAR/15 ("housing" OR "settlements" OR "living conditions")
)
```


```python
#Termlists
termlist11_1d = ["access", "obstacle", "barrier", "hinder", "hindrance", "equitab", "non-equit", "legislat", "governan", "strateg", "policy", "policies", "framework", "program",
                 "tilgang", "hinder", "hindr", "rettferdig", "urettferdig", "lovgiv", "lovgje" "politikk", "politisk", "reguler", "strateg"
                 ]

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
                #school is specified here to avoid in Norwegian university names, e.g. "Høyskole"

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

termlist11_1rtrunc = ["city"] #"city" is here due to capacity etc.

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
```
TS=
("slum" OR "slums" OR "shanty town$" OR "informal settlement*")
```


```python
#Termlists
termlist11_1s = ["shanty town", "informal settlement",
                 "uformell bosetning", "uformelle bosetninger", "uformell busetnad", "uformelle busetnad"]
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

```
#Phrase 1

TS=
(
  (
    ("safe*" OR "secure*" OR "risk*" OR "sustainab*"
    OR "access*"  OR "availab*" OR "reliab*"
    OR "afford*" OR "low cost*" OR "expensive" OR "cost-effective*"
    )
    NEAR/15 ("transport* system*" OR "transport* infrastructure*" OR "public transport*" OR "transport* network*" OR "urban* mobilit*")
  )
  AND
      ("city" OR "cities" OR "urban*" OR "municipalit*" OR "town*" OR "neighbo$rhood*" OR "village*"
      OR "infrastructure*" OR "public transport*"
      OR "pedestrian*" OR "cycl*"
      OR "road*" OR "railway*" OR "traffic*" OR "bus*" OR "taxi*"
      OR "ferry" OR "ferries" OR  "vehicl*" OR "train$" OR "underground*" OR "tube*" OR "metro*"
      OR "airport*"
      OR "travel*" OR "journey*"
      )
)

#Phrase 2
TS=
(
  (
    ("safe*" OR "secure*" OR "hazardous*" OR "dangerous*" OR "unsafe*" OR "risk*" OR "accident*")
    NEAR/5
        ("traffic*" OR "road*" OR "highway$" OR "motorway$" OR "street*"
        OR "cycling lanes" OR "cyclist$"
        OR "walkway*" OR "walking path*" OR "sidewalk*" OR "pavement*" OR "pedestrian$"
        OR "intersection$" OR "roundabout$" OR "cars" OR "car safety" OR "motorcycle$" OR "automobile$" OR "vehicle$"
        OR "driver$" OR "driving"
        OR "speed limit*"
        )
  )
  NOT ("air traffic*" OR "food*")
```

These two phrases are merged in this search. In addition we changed the structure - now, only terms that are ambiguous are combined with the "city" terms (e.g. "transport", "vehice", "driver")



```python
#Term lists

termlist11_2a = ["safe", "secure", "hazardous","sustainab", "unsafe", "dangerous","accident","access", "availab", "reliab", "afford", "low cost", "low-cost", "expensive", "cost-effective", 
                 "sikker", "trygg", "farlig", "farleg", "risiko", "bærekraftig", "berekraftig", "tilgjengelig", "pålitelig", "rimelig", "billig", "kostbar", "kostnadseffektiv"]
termlist11_2a_trunc = ["risk", "risks", "risky"] 

termlist11_2b = ["transport infrastructure", "public transport","urban mobilit", "traffic", "roadway", "street", "roundabout",
                 "highway", "motorway", "cycling lane", "cyclist", "cycle path", "bicycle lane", "walkway", "walking path", "sidewalk", "pavement","pedestrian","taxi", "ferry",
                 "the underground", "railway", "airport", 
                 "travel", "car safety", "driver safety", "safe driving", "motorcycle", "automobile", "speed limit",

                 "transportnettverk", "offentlig transport", "offentleg transport", "kollektivtransport", "transportinfrastruktur", "transportsystem", "trafikk", "rundkjøring","rundkøyring", 
                 "motorvei", "motorveg", "sykkelsti", "sykkelve", "syklist", "gangve", "fortau", "drosje", "ferge", "hurtigbåt",
                 "t-bane", "bybane", "jernbane", "flyplass", "kortbane", 
                 "sikkerhet i bil", "motorsykkel", "sjåfør", "kjøring", "kjøyring", "fartsgrense"
                 ] 
                 #"driving" combined as otherwise problematic

termlist11_2b2 = ["transport system","transport network", "driver", "vehicl",
                  "reise"]
                  #terms that need to be combined with city-terms
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
    ((Data['result_title'].str.contains(phrasedefault11_2a, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific11_2atrunc, na=False, case=False)))
    &
    (
        (Data['result_title'].str.contains(phrasedefault11_2b, na=False, case=False))
        |(Data['result_title'].str.contains(phrasespecific11_2c, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasedefault11_2b2, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault11_2d, na=False, case=False))
        )
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

```
TS=
(
  ("sustainab*" OR "inclusiv*" OR "participatory" OR "participation")
  NEAR/15 ("urbani?ation" OR "urban development")
)
```


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

```
TS=
(
  (
    ("settlement*" OR "urban*" OR "city" OR "cities" OR "metropolitan" OR "regional" OR "local" OR "municipal*" OR "neighbourhood$" OR "neighborhood$")
    NEAR/3 ("plan*" OR "manag*")
  )
  NEAR/15 ("democra*" OR "taking part" OR "sustainab*" OR "participatory" OR "participation" OR "stakeholder*")
)
```


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

termlist11_3d = ["plan", "manag",
                 "lede", "leiing", "styring", "forvalt"
                 ]
termlist11_3e = ["democra", "taking part", "sustainab", "participatory", "participation", "stakeholder",
                 "demokrat", "delta", "bærekraft", "berekraft", "interessent"
                 ]

phrasedefault11_3c = r'(?:{})'.format('|'.join(termlist11_3c))
phrasedefault11_3c_trunc = r'\b(?:{})\b'.format('|'.join(termlist11_3c_trunc))
phrasedefault11_3d = r'(?:{})'.format('|'.join(termlist11_3d))
phrasedefault11_3e = r'(?:{})'.format('|'.join(termlist11_3e))
```


```python
#Search 11_3
phrase11_3cde = Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault11_3c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault11_3c_trunc, na=False, case=False)))
    & (Data['result_title'].str.contains(phrasedefault11_3d, na=False, case=False))
    & (Data['result_title'].str.contains(phrasedefault11_3e, na=False, case=False))             
),"tempsdg11_03"] = "SDG11_03"

print("Number of results = ", len(Data[(Data.tempsdg11_03 == "SDG11_03")]))  
```


```python
test=Data.loc[(Data.tempsdg11_03 == "SDG11_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 11.4

*Strengthen efforts to protect and safeguard the world’s cultural and natural heritage*

*Styrke innsatsen for å verne og sikre verdens kultur- og naturarv*

```
TS=
(
  ("manag*" OR "maintain*" OR "conservation" OR "conserving" OR "conserve" OR "conserved" OR "conserves"
  OR "preserv*" OR "sustain" OR "protect*" OR "safeguard*"
  )
  NEAR/15
    ("cultur* heritage" OR "cultural landscape$"
    OR "heritage object$" OR "heritage building$" OR "heritage site$"
    OR "museum$" OR "archaeological place$" OR "archaeological site$" OR "historical place$" OR "historical building$" OR "historical monument$" OR "historical artefact$"
    OR "natural heritage" OR "nature formation$" OR "geopark$" OR "natural habitat$" OR "nature park$" OR "nature reserv*"
    OR "zoo$" OR "zoological garden$" OR "botanical garden$" OR "aquarium$" OR "aquaria"
    )
)
```


```python
#Termlists
termlist11_4a = ["manag", "maintain", "conservation", "conserving", "conserve", "preserv", "sustain", "protect", "safeguard",
                 "forvalt", "vedlikeh", "bevar", "konserver", "ta vare på", "oppretthold", "oppretthald", "sikre", "beskytte", "verne", "verna", "vern av", "frede", "freda", "fredning", "freding",
                 ]

termlist11_4b = ["cultural heritage", "culture heritage", "cultural landscape", "heritage object", "heritage building", "heritage site", "museum", 
                 "archaeological place", "archaeological site", "historical place", "historical building", "historical monument", "historical artefact", 
                 "natural heritage", "nature formation", "geopark", "natural habitat", "nature park", "nature reserv", "zoo", "zoological garden", "botanical garden", "aquarium", "aquaria",

                 "kulturarv", "kulturlandskap", "kulturminne", "historisk bygning", "historisk sted", 
                 "arkeologisk sted", "arkeologisk stad", "arkelogisk kulturminne", "fornminne", "arkeologisk område", "historisk monument", "historisk gjenstand", 
                 "naturarv", "naturformasjon", "naturlig habitat", "naturleg habitat", "naturpark", "nasjonalpark", "naturreservat", "dyrehage", "zoologisk hage", "botanisk hage", "akvarium", "akvarie"
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

```
TS=
(
  ( "disaster$" OR "catastrophe$" 
    OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
    OR (("natural" OR "climat*") NEAR/5 "hazard$")
    OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
    OR "drought$" OR "flood*" 
    OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
    OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
    OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
    OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
    OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 
    OR 
      (
        ("anthropogenic" 
        OR "environmental" OR "deforestation" OR "desertification" OR "degredation" OR "pollution" OR "erosion"
        OR "chemical" OR "heavy metal$" OR "pesticide$"
        OR "biological" OR "zoonotic"
        OR "technological" OR "radioactive" OR "nuclear" OR "cyber" OR "industrial" OR "construction" OR "transportation"
        ) 
        NEAR/3 ("hazard$")
      ) 
    OR "war" OR "wars" OR "armed conflict$"
    OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
    OR "financial crash*" OR "financial shock$" OR "financial disaster$" 
    OR "economic downturn$" OR "economic shock$" OR "economic disaster$"  
  )
  AND
    (
      ("death$" OR "casualt*" OR "survivors" OR "fatal*" OR "missing people" OR "missing person$")
      OR 
        (
          ("surviv*" OR "mortalit*")
          AND 
            ("people" OR "human$" OR "patient$" OR "victim$" OR "civilian$"
            OR "city" OR "cities" OR "urban" OR "municipalit*" OR "town*" OR "village*" OR "populated area*" OR "neighbo$rhood*" OR "public*" 
            OR "poverty" OR "the poor" OR "the poorest" OR "rural poor" OR "urban poor" OR "working poor" OR "destitute" OR "living in poverty"
            OR (("poor" OR "poorest" OR "low* income") NEAR/3 ("household$" OR "people" OR "children" OR "communit*"))
            OR "the vulnerable" OR "vulnerable group$" OR "vulnerable communit*" OR "marginali?ed group$" OR "marginali$ed communit*" OR "disadvantaged group$" OR "disadvantaged communit*"
            OR "slum" OR "slums" OR "shanty town$" OR "informal settlement*" OR "homeless"
            OR (("person$" OR "people$" OR "adult$") NEAR/3 ("vulnerable" OR "marginali$ed" OR "disadvantaged" OR "discriminated" OR "displaced*" OR "patient$" OR "trans" OR "intersex" OR "older" OR "old" OR "elderly" OR "retired" OR "indigenous"))
            OR "disabled" OR "disabilities" OR "disability"
            OR "elderly" OR "elders" OR "pensioners" OR "vulnerable seniors"
            OR "unemployed"
            OR "women" OR "woman" OR "girls" OR "girl"
            OR "pregnant" OR "pregnancy" OR "maternity" OR "child" OR "children" OR "infant$" OR "babies" OR "newborn$" OR "toddler$" OR "youth$"
            OR "sexual minorit*" OR "LGBT*" OR "lesbian$" OR "gay" OR "bisexual" OR "transgender*"
            OR "living with HIV" OR "living with AIDS"
            OR "ethnic minorit*" OR "minority group$" OR "refugee$" OR "migrant$" OR "immigrant$" OR "asylum*"
            OR "indigenous group$"
            )
        )
    )
) NOT TS=("death$" NEAR/3 ("tree" OR "trees" OR "leaf" OR "cell"))
```


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
termlist11_5l = ["death", "casualt", "survivors", "fatal", "missing people", "missing person",
                 "død", "daud" "offer", "ofre", "overlevende", "overlevande", "savnede", "savnet", "sakna"]
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
#The NOT-part at the end of WoS string is not included, as probably not needed/useful in title searching
```


```python
#Search 11_5
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault11_5a, na=False, case=False))
        |
         (
            (Data['result_title'].str.contains(phrasedefault11_5b, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault11_5c, na=False, case=False))
         )
        | 
          (
            (Data['result_title'].str.contains(phrasedefault11_5d, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault11_5e, na=False, case=False))  
          )
        | 
          (
            (Data['result_title'].str.contains(phrasedefault11_5j, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault11_5k, na=False, case=False))  
          )          
        | (Data['result_title'].str.contains(phrasedefault11_5f, na=False, case=False))
        | (Data['result_title'].str.contains(phrasedefault11_5ftrunc, na=False, case=False))
      
    )
    &
    (
        (Data['result_title'].str.contains(phrasedefault11_5l, na=False, case=False))
        |
        (
            (Data['result_title'].str.contains(phrasedefault11_5m, na=False, case=False))
            &
            ( 
              (Data['result_title'].str.contains(phrasedefault11_5n, na=False, case=False))
              |
              (
                (Data['result_title'].str.contains(phrasedefault11_5o, na=False, case=False))
                & (Data['result_title'].str.contains(phrasedefault11_5p, na=False, case=False)) 
              )
              |
              (
                (Data['result_title'].str.contains(phrasedefault11_5q, na=False, case=False))
                & (Data['result_title'].str.contains(phrasedefault11_5r, na=False, case=False)) 
              )
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

```
TS=
(
  ( 
    ("disaster$" OR "catastrophe$" 
    OR ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
    OR (("natural" OR "climat*") NEAR/5 "hazard$")
    OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
    OR "drought$" OR "flood*" 
    OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
    OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
    OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
    OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
    OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$")) 
    OR 
      (
        ("anthropogenic" 
        OR "environmental" OR "deforestation" OR "desertification" OR "degredation" OR "pollution" OR "erosion"
        OR "chemical" OR "heavy metal$" OR "pesticide$"
        OR "biological" OR "disease" OR "zoonotic"
        OR "technological" OR "radioactive" OR "nuclear" OR "cyber" OR "industrial" OR "construction" OR "transportation"
        ) 
        NEAR/3 ("hazard$")
      ) 
    OR "war" OR "wars" OR "armed conflict$"
    OR (("volatil*" OR "unstable" OR "instability" OR "unrest") NEAR/5 ("political$" OR "civil"))
    OR "financial crash*" OR "financial shock$" OR "financial disaster$" 
    OR "economic downturn$" OR "economic shock$" OR "economic disaster$"
    )  
  )
  AND ("domestic product$" or "gdp$" or "ggdp$" or "ggp$" or "gross global produc$")
)
```


```python
#Termlists
                 
termlist11_52l = ["domestic product", "gross global produc",
                 "nasjonalprodukt", "bnp"]
termlist11_52ltrunc = ["gdp", "gpp", "ggdp"]
                                          
phrasedefault11_52l = r'(?:{})'.format('|'.join(termlist11_52l))
phrasedefault11_52ltrunc = r'\b(?:{})\b'.format('|'.join(termlist11_52ltrunc))
#acronyms not truncated to avoid results on gdpr
```


```python
#Search 11_5
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault11_5a, na=False, case=False))
        |
         (
            (Data['result_title'].str.contains(phrasedefault11_5b, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault11_5c, na=False, case=False))
         )
        | 
          (
            (Data['result_title'].str.contains(phrasedefault11_5d, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault11_5e, na=False, case=False))  
          )
        | (Data['result_title'].str.contains(phrasedefault11_5f, na=False, case=False))
        | (Data['result_title'].str.contains(phrasedefault11_5ftrunc, na=False, case=False))
      
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
```
TS=
(
  ("environment* impact*" OR "footprint$" OR "foot print$")
   NEAR/15 ("city" OR "cities" OR "urban" OR "municipalit*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*" OR "public*")
)
```


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
```
TS=
(
  ("smog*" OR "air pollution" OR "suspended particles" OR "particulate matter" OR "pm2.5" OR "pm10")
  NEAR/15 ("city" OR "cities" OR "urban" OR "municipalit*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*" OR "public*")
)
OR
TS=
(
   ("clean air" OR "air quality")
   NEAR/15 ("city" OR "cities" OR "urban" OR "municipalit*" OR "human settlement*" OR "town*" OR "communit*" OR "village*" OR "populated area*" OR "public*")
)
```


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
```
TS=
(
  ("solid waste" OR "bulky waste" OR "household waste" OR "domestic waste" OR "commercial waste" OR "industrial waste"
  OR "MSW"
  OR ("waste" NEAR/15 ("end of life" OR "eol" OR "end of chain" OR "eoc"))
  OR "garbage" OR "rubbish"
  )
  AND ("waste" OR "garbage" OR "rubbish")
)
```


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
```
TS=
(
   ("environmental impact" OR "environmental assess*" OR "footprint*" OR "foot print*")
    NEAR/15 (("waste" OR "garbage" OR "rubbish") NEAR/3 ("manag*" OR "collect*"))
)
```



```python
#Term lists

termlist11_6f = ["environmental impact", "impact on the environment", "impacts on the environment","environmental assess", "footprint","foot print",
                 "miljøpåvirk", "fotavtrykk", "påvirke miljø", "påverke miljø", "miljøvurdering"]
  
termlist11_6g = ["waste", "garbage", "rubbish", 
                 "avfall", "søppel", "boss"
                 ]

termlist11_6h = ["manag", "collect", "reuse", "re-use", "composting",
                 "håndter", "handter", "innsamling", "gjennvin", "gjenbruk", "resirkuler", "renovasjon", "komposter",
                 ] 


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

```
TS=
(
  ("safe" OR "inclus*" OR "access*" OR "unrestrict*")
  NEAR/15
      ("green space$" OR "recreational area$" OR "public area$" OR "public space$" OR "public garden$"
      OR "community garden$" OR "allotment garden$" OR "urban allotment$" 
      OR ("park$" NEAR/15 ("city" OR "cities" OR "metropolitan" OR "town$" OR "built-up area$" OR "urban*" OR "neighbourhood$" OR "neighborhood$"))
      )
)
```


```python
#Termlists
termlist11_7a = ["safe", "inclus", "access", "unrestrict",
                 "trygg", "sikker", "inkluder", "inklus", "tilgang", "adgang", "uhindr", "ubegrens"]

termlist11_7b = ["green space", "recreational area", 
                 "public area", "public space", "public open space",
                 "public facilit",
                 "library area", "library space", "libraries", "community cent", "community space",
                 "public garden", "community garden", "allotment garden", "urban allotment",

                 "grønne område", "grøntområde", "parkområde", "friluftsområde", "fritidsområde", 
                 "offentleg område", "offentlig område" "offentlig sted", "offentleg stad", "offentlig plass", "offentleg plass", "byrom", 
                 "offentlig fasilit", "offentleg fasilit",
                 "bibliotekareal", "bibliotekrom", "bibliotekbygg", "samfunnshus",
                 "bypark", "kolonihage", "parsellhage", "hageparsell", "felleshage"
                 ]
termlist11_7c = ["park", "parks", 
                 "parker"]

termlist11_7d =  ["cities","city", "megacit", "urban", "metropolitan", 
                 "town", "village", "suburb", 
                 "municipal", "district", "region", "human settlement", "built-up area", "populated area",
                 "community", "neighborhood", "neighbourhood", 

                 "byer", "byar", "byen", "bydel", "byområde", "storby", "småby", "landsby", "kystby", "byplan", "byutvik", "bystruktur", "bymiljø", 
                 "bygd", "grend", "nærområde", "drabant",
                 "kommun", "fylke", "distrikt", "befolka område", "befolket område", "tettsted", "tettstad",
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
        |
        (
            (Data['result_title'].str.contains(phrasedefault11_7c, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault11_7d, na=False, case=False))
        )
    )              
),"tempsdg11_07"] = "SDG11_07"

print("Number of results = ", len(Data[(Data.tempsdg11_07 == "SDG11_07")])) 
```


```python
test=Data.loc[(Data.tempsdg11_07 == "SDG11_07"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2

```
TS=
(
  ("restrict*" OR "inaccess*" OR "equal access"
  OR "inequalit*" OR "inequit*" OR "equitab*" OR "justice" OR "injustice"
  OR "discriminat*" OR "exclu*" OR "harass*" OR "assault*" OR "unsafe"
  )
  NEAR/15
      ("green space$" OR "recreational area$" OR "public area$" OR "public space$" OR "public garden$"
      OR "community garden$" OR "allotment garden$" OR "urban allotment$"
      OR ("park$" NEAR/15 ("city" OR "cities" OR "metropolotan" OR "town$" OR "built-up area$" OR "urban*" OR "neighbourhood$" OR "neighborhood$"))
      )
)
```

Here, as it is a title search, we have decided to drop the combination of "parks" + "cities", so that "parks" can be alone.


```python
#Termlists
termlist11_7e = ["restrict", "inaccess", "equal access", "inequalit", "inequit", "equitab", "justice", "injustice", 
                 "discriminat", "exclud", "harass", "assault", "unsafe"
                 "restrik", "utilgjenge", "allmen tilgang", "allmenn adgang", "lik adgang", "lik tilgang", "uhindr", "ubegrens", "ulikhet", "rettferd", 
                 "diskrimin", "utesteng", "utenforskap", "eksklude", "trakasser", "mobb", "overfall", "angrep", "utrygg"
                 ]

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

```
TS=
(
  (
    ("national" OR "regional")
    NEAR/3 ("plan" OR "planning" OR "plans" OR "strateg*" OR "framework$" OR "program" OR "programs" OR "policy" OR "policies" OR "cooperat*")
  )
  NEAR/15
      ("city" OR "cities" OR "urban*" OR "town$" OR "village$"
      OR "built-up area$" OR "neighbourhood$" OR "neighborhood$" OR "settlement$"
      OR "rural area$" OR "rural development"
      )
)
```


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

```
TS=
(
  ("sendai framework" OR "disaster risk reduction"
  OR "cancun adapation framework"
  OR "readiness and preparatory support programme" OR "readiness programme"
  OR
    (
      ("plan" OR "plans" OR "planning" OR "strateg*" OR "program$" OR "programme$" OR "policy" OR "policies" OR "governance" OR "framework$")
      NEAR/3 ("disaster$" OR "risk$" OR "climate change" OR "climatic change$" OR "global warming" OR "changing climate" OR "climate action" OR "climate mitigation")
    )
  )
  NEAR/15
      ("city" OR "cities" OR "urban*" OR "metropolitan" OR "town$" OR "village$"
      OR "built-up area$" OR "neighbourhood$" OR "neighborhood$" OR "settlement$"
      OR "rural area$" OR "rural development"
      )
)
```


```python
#Termlists
termlist11_Ba = ["sendai", "disaster risk reduction", "cancun adapation framework", "readiness and preparatory support programme", "readiness programme",
                 "katastrofeforebygging", "cancun-avtal", "cancun avtal", "klimatilpas", "forebyggingstiltak"
                 ]
termlist11_Bb = ["plan ", "plans", "planning", "strateg", "program", "policy", "policies", "governance", "framework",
                 "rammeverk", "politikk", "politisk", "forvalt", "styring", "ledelse", "leiing", "retningslin"
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



```
TS=
(
  ("local building material$" OR "local construction material$"
  OR "sustainable architecture" OR "resilient architecture"
  OR
    (
      ("buildings" OR "sustainable building" OR "masonry"
      OR
        (
          ("construction" OR "building")
           NEAR/5 ("material$" OR "method$" OR "technique$" OR "industry" OR "industries" OR "company" OR "companies" OR "home$" OR "house$" OR "residential" OR "sector")
        )
      )
      NEAR/15
          ("sustainab*" OR "ecofriendly" OR "eco friendly" OR "environmentally friendly" OR "resilien*"
          OR ("local*" NEAR/3 "materials") OR "locally available" OR "native" OR "traditional"
          )
    )          
  )
  AND
    (***LDCs***
    )
)
```


```python
#Term lists

termlist11_6i = ["sustainable architecture","resilient architecture","sustainable building","sustainable construction",
                 "local building material", "local construction material", "locally available building material",
                 "bærekraftig arkitektur","berekraftig arkitektur","bærekraftig bygning","berekraftig bygning","bærekraftig konstruksjon", "berekraftig konstruksjon",
                 "lokale bygningsmatrial","lokale konstruksjonsmaterial"
                 ] 
  
termlist11_6j = ["sustainable", "eco-friendly", "ecofriendly", "environmentally friendly", "resili",
                 "local material", "locally available", "native", "traditional",
                 "bærekraftig", "berekraftig", "miljøven", "økoven", "tradisjonel", "lokal"
                 ]
termlist11_6k = ["construction", "buildings", "building material", "building technique", "building method", "building industry", "home building", "building homes",
                 "konstruksjon", "bygge", "byggningsbransj", "byggebransj"
                 ]
                 #"building" causes issues (capacity building etc.)

phrasedefault11_6i = r'(?:{})'.format('|'.join(termlist11_6i))
phrasedefault11_6j = r'(?:{})'.format('|'.join(termlist11_6j))
phrasedefault11_6k = r'(?:{})'.format('|'.join(termlist11_6k))
```


```python
#Search 1 - in LDCs
Data.loc[(
    (
      (Data['result_title'].str.contains(phrasedefault11_6i, na=False, case=False))
      | 
      (
          (Data['result_title'].str.contains(phrasedefault11_6j, na=False, case=False))
          & (Data['result_title'].str.contains(phrasedefault11_6k, na=False, case=False))
      )
    )
    & (Data['LDCs']==True)
),"tempsdg11_c"] = "SDG11_c"
```


```python
print("Number of results = ", len(Data[(Data.tempsdg11_c == "SDG11_c")]))
```

### SDG 11 mentions

```
TS=
("SDG 11" OR "SDGs 11" OR "SDG11" OR "sustainable development goal$ 11"
OR ("sustainable development goal$" AND "goal 11")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 11")
  AND ("sustainable cities")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 11")
    NEAR/15 ("cities")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
```
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

## SDG 13

### SDG 13.1


```
TS=
(
  (
    ("coping" OR "cope" OR "adapt*" OR "resilien*" OR "mitigat*" OR "risk reduction" OR "preparedness" OR "preparing" OR "preparation")
    OR  
      (
        ("mitigat*" OR "prevent*" OR "reduc*" OR "decreas*" OR "minimis*" OR "minimiz*" OR "manag*")
        NEAR/5 ("impact$" OR "vulnerab*")
      )
    OR
    (
      ("disaster$" OR "risk$")
      NEAR/3
        ("plan" OR "plans" OR "planning" OR "strateg*" OR "program$" OR "programme$" OR "policy" OR "policies" OR "governance"
        OR "reduc*" OR "manag*" OR "medical response$" OR "relief"
        )
    )
    OR "sendai framework"
    OR "cancun adapation framework"
    OR "readiness and preparatory support programme" OR "readiness programme"
  )  
  NEAR/15
      (
        ("extreme$" NEAR/3 ("climat*" OR "weather" OR "precipitation" OR "rain" OR "snow" OR "temperature$" OR "storm$" OR "wind$"))
        OR (("natural" OR "climat*") NEAR/5 ("hazard$" OR "catastrophe$" OR "disaster$"))
        OR "rogue wave$" OR "tsunami$" OR "tropical cyclone$" OR "typhoon$" OR "hurricane$" OR "tornado*"
        OR "drought$" OR "flood*"
        OR "avalanche$" OR "landslide$" OR "land-slide$" OR "rockslide$" OR "rock-slide$" OR "rockfall$" OR "surface collapse$" OR "mudflow$" OR "mud-flow$"
        OR "cold spells" OR "cold wave$" OR "dzud$" OR "blizzard$" OR "heatwave$" OR "heat-wave$"
        OR "earthquake$" OR "volcanic activity" OR "volcanic emission$" OR "volcanic eruption$" OR "ash fall" OR "tephra fall"
        OR "wildfire*" OR "wild-fire*" OR "forest fire*" OR "forestfire*"
        OR ("sea level" NEAR/3 ("chang*" OR "rising" OR "rise$"))
      )
)

```


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
termlist13_1e = ["plan", "strateg", "program", "policy", "policies", "governance", "reduc", "manag", "medical response", "relief",
                 "politikk", "retningslin", "styring", "ledelse", "leiing", "reduser", "reduksjon", "medisinsk", "bistand", "støtte", "stønad"]
termlist13_1f = ["sendai", "cancun", "readiness and preparatory support programme", "readiness programme",
                 "beredskap", "katastrofe"]
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
                 "havnivåstigning", "stormflo", 
                ] 

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
            |
         (
            (Data['result_title'].str.contains(phrasedefault13_1b, na=False, case=False))&
            (Data['result_title'].str.contains(phrasedefault13_1c, na=False, case=False))
         )
            |
         (
           (Data['result_title'].str.contains(phrasedefault13_1d, na=False, case=False))&
           (Data['result_title'].str.contains(phrasedefault13_1e, na=False, case=False))   
         )
            |
          (Data['result_title'].str.contains(phrasedefault13_1f, na=False, case=False))
        )
           &
      (
        (
            (Data['result_title'].str.contains(phrasedefault13_1g, na=False, case=False))&
            (Data['result_title'].str.contains(phrasedefault13_1h, na=False, case=False))
        )
           |
        (
            (Data['result_title'].str.contains(phrasedefault13_1i, na=False, case=False))&
            (Data['result_title'].str.contains(phrasedefault13_1j, na=False, case=False))
        )
          |
          (Data['result_title'].str.contains(phrasedefault13_1k, na=False, case=False))
          |
       (
          (Data['result_title'].str.contains(phrasedefault13_1l, na=False, case=False))&
          (Data['result_title'].str.contains(phrasedefault13_1m, na=False, case=False))
       )
     )
),"tempsdg13_01"] = "SDG13_01"

print("Number of results = ", len(Data[(Data.tempsdg13_01 == "SDG13_01")])) 
```


```python
test=Data.loc[(Data.tempsdg13_01 == "SDG13_01"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13.2


#### Phrase 1

```
TS=
(
  ("climate change$" OR "global warming" OR "climatic change$" OR "changing climate"
  OR "climate measures" OR "climate action" OR "climate adaptation" OR "climate mitigation" OR "climate resilience"
  OR ("warming" NEAR/3 ("climat*" OR "atmospher*" OR "ocean"))
  OR "GHG" OR "greenhouse gas" OR "greenhouse gases"
  OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$"
  OR "methane" OR "CH4" OR "nitrous oxide" OR "NOX" OR "N2O" OR "carbon dioxide" OR "CO2" OR "hydrofluorocarbons" OR "HFCs" OR "perfluorocarbons" OR "PFCs" OR "sulphur hexafluoride" OR "sulfur hexafluoride" OR "SF6"
  )
  AND
    (
      ("national*" OR "state" OR "federal" OR "domestic" OR "sectoral" OR "multi level" OR "multilevel")
      NEAR/5
          ("program$" OR "programme$" OR "strateg*" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans"
          OR "policy" OR "policies" OR "law$" OR "legislat*" OR "governance" OR "mandate$"
          OR "nationally determined contribution$" OR "adaptation communication$" OR "monitoring and evaluation" OR "adaptation committee"
          )
    )
  AND
    ("climate" OR "global warming" OR "climatic change$"
    OR ("warming" NEAR/3 ("atmospher*" OR "ocean"))
    OR "GHG" OR "greenhouse gas" OR "greenhouse gases" OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$"
    OR "sea level rise"
    )
)
```




```python
# Term lists
termlist13_2a = ["climate change", "global warming", "climatic change", "changing climate", "climate measures", "climate action", "climate adaptation", "climate mitigation", 
                 "climate resilience",
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
                 "nasjonalt fastsatt bidrag", "nasjonalt fastsatte bidrag", "nasjonalt fastsette bidrag", 
                 "tilpasningskommunikasjon", "tilpassingskommunikasjon", "komite"]   
termlist13_2n = ["climate", "global warming", "climatic change", 
                 "klima", "global oppvarming"]
termlist13_2o = ["warming", 
                 "oppvarming"]
termlist13_2p = ["atmosphere", "ocean", 
                 "atmosfære", "hav"]
termlist13_2q = ["GHG", "greenhouse gas", "carbon footprint", "CO2 footprint", "carbon emission", "CO2 emission", "sea level rise",
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
     (Data['result_title'].str.contains(phrasedefault13_2a, na=False, case=False))|
     (
        (Data['result_title'].str.contains(phrasedefault13_2b, na=False, case=False))&
        (Data['result_title'].str.contains(phrasedefault13_2j, na=False, case=False))
     )
    |
        (Data['result_title'].str.contains(phrasedefault13_2k, na=False, case=False))   
 )
   & 
   (
     (
        (Data['result_title'].str.contains(phrasedefault13_2l, na=False, case=False))&
        (Data['result_title'].str.contains(phrasedefault13_2m, na=False, case=False))  
     )
   )
   &
   (
        (Data['result_title'].str.contains(phrasedefault13_2n, na=False, case=False)) |
    (
        (Data['result_title'].str.contains(phrasedefault13_2o, na=False, case=False))&
        (Data['result_title'].str.contains(phrasedefault13_2p, na=False, case=False))
    ) 
  |
        (Data['result_title'].str.contains(phrasedefault13_2q, na=False, case=False))
   )   
),"tempsdg13_02"] = "SDG13_02"

print("Number of results = ", len(Data[(Data.tempsdg13_02 == "SDG13_02")]))  
```


```python
test=Data.loc[(Data.tempsdg13_02 == "SDG13_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2


```
TS=
(
  (
    ("global temperature" OR "surface temperature" OR "sea-level" OR "sea level"
    OR "sea ice*" OR "sea-ice" OR "glacial" OR "glacier$" OR "permafrost"
    OR "ocean acidification" OR "ocean heat content"
    )
    NEAR/15
        ("action$" OR "sustainab*" OR "adapt*" OR "cope" OR "coping" OR "resilien*" OR "mitigat*"
        OR "impact$" OR "effect$" OR "consequence$" OR "influence$" OR "vulnerab*"
        )
  )
  AND
      (
        ("national*" OR "state" OR "federal" OR "domestic" OR "sectoral" OR "multi level" OR "multilevel")
        NEAR/5
            ("program$" OR "programme$" OR "strateg*" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans"
            OR "policy" OR "policies" OR "law$" OR "legislat*" OR "governance" OR "mandate$"
            OR "nationally determined contribution$" OR "adaptation communication$" OR "monitoring and evaluation" OR "adaptation committee"
            )
      )
)
```



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
                 "nasjonalt fastsatt bidrag", "nasjonalt fastsatte bidrag", "nasjonalt fastsette bidrag",
                 "tilpasningskommunikasjon", "tilpassingskommunikasjon", "komite"]


phrasedefault13_2c = r'(?:{})'.format('|'.join(termlist13_2c))
phrasedefault13_2d = r'(?:{})'.format('|'.join(termlist13_2d))
phrasedefault13_2e = r'(?:{})'.format('|'.join(termlist13_2e))
phrasedefault13_2f = r'(?:{})'.format('|'.join(termlist13_2f))
```


```python
#Search13_2cdef
Data.loc[(
                  (Data['result_title'].str.contains(phrasedefault13_2c, na=False, case=False))&
                  (Data['result_title'].str.contains(phrasedefault13_2d, na=False, case=False))&
                  (Data['result_title'].str.contains(phrasedefault13_2e, na=False, case=False))&
                  (Data['result_title'].str.contains(phrasedefault13_2f, na=False, case=False))
),"tempsdg13_02"] = "SDG13_02"

print("Number of results = ", len(Data[(Data.tempsdg13_02 == "SDG13_02")]))  
```


```python
test=Data.loc[(Data.tempsdg13_02 == "SDG13_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 3

```
TS=
(
  ("Kyoto protocol" OR "Paris Agreement"
  OR "COP 21" OR "COP21" OR "COP 22" OR "COP22" OR "COP 23" OR "COP23" OR "COP 24" OR "COP24" OR "COP 25" OR "COP25" OR "COP 26" OR "COP26" OR "COP 27" OR "COP27"
  OR "UNFCCC" OR "United Nations Framework Convention on Climate Change"
  OR "Cancun adaptation framework"
  )
  AND
    (
      ("national*" OR "state" OR "federal" OR "domestic" OR "sectoral" OR "multi level" OR "multilevel")
      NEAR/5
          ("program$" OR "programme$" OR "strateg*" OR "framework$" OR "initiative$" OR "plan" OR "planning" OR "plans"
          OR "policy" OR "policies" OR "law$" OR "legislat*" OR "governance" OR "mandate$"
          )
    )
)
```


```python
# Term lists
termlist13_2g = ["Kyoto protocol", "kyoto", "Paris agreement", "cop 21", "cop21", "cop 22", "cop22", "cop 23", "cop23",
                 "cop 24", "cop24", "cop 25", "cop25", "cop 26", "cop26", "cop 27", "cop27",
                 "unfccc", "United Nations Framework Convention on Climate Change", "Cancun adaptation framework",
                 "kyotoprotokoll", "parisavtale", "paris-avtale", "parisavtala", "paris-avtala", "klimakonvensjon", "Cancun"]
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
          (Data['result_title'].str.contains(phrasedefault13_2g, na=False, case=False))|
          (Data['result_title'].str.contains(phrasespecific13_2gtrunk, na=False, case=False))
      )
      &
        (
          (Data['result_title'].str.contains(phrasedefault13_2h, na=False, case=False))&
          (Data['result_title'].str.contains(phrasedefault13_2i, na=False, case=False))
        )
),"tempsdg13_02"] = "SDG13_02"

print("Number of results = ", len(Data[(Data.tempsdg13_02 == "SDG13_02")]))  
```


```python
test=Data.loc[(Data.tempsdg13_02 == "SDG13_02"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13.3

#### Phrase 1

```
TS=
(
  ("capacity" OR "capabilit*"
  OR "educat*" OR "curriculum" OR "curricula" OR "teacher training" OR "climate literacy"
  OR "research" OR "knowledge" OR "skills" OR "tools" OR "competenc*" OR "expertise" OR "training"
  OR "awareness" OR "responsibilit*"
  OR "infrastructure$" OR "technolog*" OR "early warning system$"
  OR "communication" OR "collaboration" OR "cooperation" OR "co operation" OR "social network$" OR "information network$"
  OR "economic resources" OR "financial resources" OR "human resource$"
  OR (("institutional" OR "administrative" OR "policy" OR "governance") NEAR/5 ("structure$" OR "values" OR "practices" OR "arrangement$" OR "resources"))
  )  
  NEAR/15      
      (
        (
          ("climate" OR "global warming" OR "climatic change$" OR "sea level rise")
          NEAR/5  
              ("action$" OR "sustainab*" OR "mitigat*" OR "adapt*" OR "cope" OR "coping" OR "resilien*"
              OR "early warning" OR "warning system$" OR "preparedness" OR "risk$" OR "vulnerab*"
              OR "awareness" OR "climate education" OR "climate sensitive education" OR "climate change education" OR "climate literacy"
              OR "solutions" OR "problems"
              OR
                (
                  ("reduc*" OR "minimi*" OR "decreas*" OR "limit" OR "alleviat*")
                  NEAR/2 ("impact$" OR "effect$" OR "consequence$")        
                )
              )
        )
        OR
          (
            ("reduc*" OR "minimi*" OR "limit" OR "limiting" OR "decreas*" OR "lower" OR "mitigat*"
            OR "alleviat*" OR "tackl*" OR "combat*" OR "prevent*" OR "stop*" OR "avoid*"
            )
              NEAR/5
                  ("GHG" OR "greenhouse gas" OR "greenhouse gases" OR "carbon footprint" OR "CO2 footprint" OR "carbon emission$" OR "CO2 emission$")
          )   
      )
)
```


```python
# Term lists
termlist13_3a = ["capacity", "capabilit", "educat", "curriculum", "curricula", "teacher training", "climate literacy", "research", "knowledge", "skills",
                 "tools", "competenc", "expertise", "training", "awareness", "responsibilit", "infrastructure", "technolog", "early warning system",
                 "communication", "collaboration", "cooperation", "co operation", "social network", "information network", 
                 "economic resources", "financial resources", "human resource",
                 
                 "kapasitet", "evne", "utdann", "pensum", "læreplan", "fagplan", "emneplan", "studieplan", "lærerutdann", "lærarutdann",
                 "klimakompetanse", "forskning", "forsking", "kunnskap", "ferdighet", "ferdigheit",
                 "verktøy", "kompetanse", "ekspertise", "bevisst", "medvett", "medvit", "ansvar", "infrastruktur", "teknolog", 
                 "tidlig varsling", "tidleg varsling", "varslingssystem"
                 "kommunikasjon", "samarbeid", "sosiale nettverk", "informasjonsnettverk",
                 "økonomiske ressurs", "finansielle ressurs", "menneskelige ressurser", "menneskelege ressursar"]
termlist13_3b = ["institutional", "administrativ", "policy", "governance",
                 "institusjonell", "politikk", "styring", "ledelse", "leiing"] 
termlist13_3c = ["structure", "values", "practices", "arrangement", "resources",
                 "struktur", "verdi", "praksis", "ressurs"]
termlist13_3d = ["climate", "global warming", "climatic change", "sea level rise",
                 "klima", "global oppvarming", "klimaendring", "klimaforandring", "havnivåstigning"]
termlist13_3e = ["action", "sustainab", "mitigat", "adapt", "cope", "coping", "resilien", "early warning", "warning system", "preparedness", "risk", "vulnerab", "awareness", 
                 "climate education", "climate sensitive education", "climate change education", "climate literacy", "solutions", "problem"
                 "handl", "bærekraft", "berekraft", "mink", "demp", "reduser", "reduksjon", "tilpas", "takl", "klare", "greie", "fikse", "overkomme", 
                 "tidlig varsling", "tidleg varsling", "varslingssystem",
                 "forbered", "førebu", "risik", "sårbar", "bevisst", "oppmerks",
                 "klimautdann", "klimaopplær", "klimakomp", "løsning", "løysing"]
termlist13_3f = ["reduc", "minimi", "decreas", "limit", "alleviat",
                 "reduser", "reduksjon", "minimer", "mink", "grens", "lett"]
termlist13_3g = ["impact", "effect", "consequence",
                 "innflytelse", "innvirkning", "innverknad", "påvirk", "påverk", "betydning", "effekt", "konsekvens", "følge", "følgje"]
termlist13_3h = ["reduc", "minimi", "limit",  "decreas", "lower", "mitigat", "alleviat", "tackl", "combat", "prevent", "stop", "avoid",
                 "reduser", "reduksjon", "minimer", "mink", "grens", "lett", "takl", "klare", "greie", "fikse", "overkomme", "kjempe", "hindr", "stopp", "stogg", "unngå"]
termlist13_3i = ["GHG", "greenhouse gas", "carbon footprint", "CO2 footprint", "carbon emission", "CO2 emission",
                 "drivhusgass", "klimagass", "karbonfotavtrykk", "karbonavtrykk", "karbonutsl", "karbondioksidutsl", "co2-utsl"]            

phrasedefault13_3a = r'(?:{})'.format('|'.join(termlist13_3a))
phrasedefault13_3b = r'(?:{})'.format('|'.join(termlist13_3b))
phrasedefault13_3c = r'(?:{})'.format('|'.join(termlist13_3c))
phrasedefault13_3d = r'(?:{})'.format('|'.join(termlist13_3d))
phrasedefault13_3e = r'(?:{})'.format('|'.join(termlist13_3e))
phrasedefault13_3f = r'(?:{})'.format('|'.join(termlist13_3f))
phrasedefault13_3g = r'(?:{})'.format('|'.join(termlist13_3g))
phrasedefault13_3h = r'(?:{})'.format('|'.join(termlist13_3h))
phrasedefault13_3i = r'(?:{})'.format('|'.join(termlist13_3i))
```


```python
## Search 13_3abcdefghi
Data.loc[(
    ( 
      (Data['result_title'].str.contains(phrasedefault13_3a, na=False, case=False))|
      (
         (Data['result_title'].str.contains(phrasedefault13_3b, na=False, case=False))
         &
         (Data['result_title'].str.contains(phrasedefault13_3c, na=False, case=False))
      )
    )
    &
     (
        ( 
         (Data['result_title'].str.contains(phrasedefault13_3d, na=False, case=False))
           &
            (
              (Data['result_title'].str.contains(phrasedefault13_3e, na=False, case=False))
            |
              (
                (Data['result_title'].str.contains(phrasedefault13_3f, na=False, case=False))
                &
                (Data['result_title'].str.contains(phrasedefault13_3g, na=False, case=False))
              )  
            )   
          |
          (
              (Data['result_title'].str.contains(phrasedefault13_3h, na=False, case=False))
               &
              (Data['result_title'].str.contains(phrasedefault13_3i, na=False, case=False))
          )
        )
       )
),"tempsdg13_03"] = "SDG13_03"

print("Number of results = ", len(Data[(Data.tempsdg13_03 == "SDG13_03")]))

```


```python
test=Data.loc[(Data.tempsdg13_03 == "SDG13_03"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13.a

```
TS=
(
  (
    ("transparency" OR "accountability" OR "governance" OR "allocation$" OR "misallocation" OR "corruption"
    OR "operationali*" OR "capitali*" OR "mobilis*" OR "mobiliz*"
    OR "contribut*" OR "commitment$" OR "negotiation$"
    OR ("financial mechanism" NEAR/15 ("UNFCCC" OR "convention"))
    OR "donor$" OR "donation$" OR "donate"
    OR "annex II party" OR "annex II parties" OR "developed countr*" OR "developed nation$" OR "OECD"
    OR ****LMICS****
    )
    NEAR/15
        ("climate financ*" OR "climate aid" OR "climate loan$" OR "climate fund*" OR "climate bond$"
        OR "green climate fund" OR "Least Developed Countries Fund" OR "LDCF" OR "Special Climate Change Fund" OR "SCCF" OR "adaptation fund$" OR "adaptation financ*"
        OR
          ("climat*"
          NEAR/15
              ("financing" OR "fund" OR "funds" OR "funding"
              OR (("economic" OR "financial*" or "monetary") NEAR/3 ("support*" or "assist*" OR "resources"))
              OR "ODA" OR "cooperation fund$" OR "development spending"
              OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance" OR "finance" OR "grant$" OR "investment$"))
              )
          )
        )
  )
  AND
      ("climate change" OR "global warming" OR "climate action" OR "climate mitigation" OR "climate adaptation"
      OR "climate financ*" OR "climate aid" OR "climate loan$" OR "climate fund*" OR "climate bond$"
      OR "green climate fund" OR "Least Developed Countries Fund" OR "LDCF" OR "Special Climate Change Fund" OR "SCCF" OR "adaptation fund$" OR "adaptation financ*"
      )
)
```



```python
# Term lists

termlist13_a1 =  ["transparency", "accountability", "governance", "allocation", "misallocation", "corruption", "operationali", "capitali,", "mobilis", "mobiliz", "contribut",
                "commitment", "negotiation", "donor", "donation", "donate", "annex II party", "annex II parties",
                
                "transparen", "ansvarlig", "ansvarleg", "styring", "ledelse", "leiing", "korrupsjon", "muting", "bestikke", "tildel", "fordel", "utdel", "alloker", "operasjonaliser", "kapital", "mobiliser", "bidra",
                "forplikt", "forhandl", "giver", "givar", "gjevar", "donasjon", "doner"
               ]
termlist13_a2 = ["financial mechanism", 
                 "finansiering"]
termlist13_a3 = ["UNFCCC", "convention", 
                 "FN", "konvensjon"]
termlist13_a4 = ["climate financ", "climate aid", "climate loan", "climate fund", "climate bond", "least developed countries fund", "LDCF", "special climate change fund", "SCCF",
                 "adaptation fund", "adaptation financ",
                 "klimafinans", "klimahjelp", "klimastø", "klimalån", "klimafond", "klimaobligasjon", "klimainvesteringsfond", "tilpasningsfond", "tilpassingsfond", 
                 "tilpasningsfinans", "tilpassingsfinans"]
termlist13_a5 = ["climate", 
                 "klima"]
termlist13_a6 = ["financing", "fund", 
                 "finansier", "fond"]        
termlist13_a7 = ["economic", "financial", "monetary", 
                 "økonomi", "finansiell", "monetær", "penge"] 
termlist13_a8 = ["support", "assist", "resources", 
                 "støtte", "stønad", "hjelp", "assistanse", "ressurs"]
termlist13_a9 = ["ODA", "cooperation fund", "development spending", 
                 "samarbeidsfond", "bistand"] 
termlist13_a10 = ["international", "development", "foreign", 
                  "internasjonal", "utvikling", "utenlands", "utalands", "utanlands"]
termlist13_a11 = ["aid", "assistance", "finance", "grant", "investment", 
                  "hjelp", "assistanse", "finansier", "støtte", "stønad", "bidrag", "bistand", "invester"]      
termlist13_a12 = ["climate", "global warming", 
                  "green climate fund", "least developed countries fund", "LDCF", "special climate change fund", "SCCF", "adaptation fund", "adaptation financ",
                  "klima", "global oppvarming", "tilpasningsfond", "tilpassingsfond"]
                       
phrasedefault13_a1 = r'(?:{})'.format('|'.join(termlist13_a1))
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
```


```python
# Search
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault13_a1, na=False, case=False))
        |(Data['LMICs']==True)
        |
        (
            (Data['result_title'].str.contains(phrasedefault13_a2, na=False, case=False))
            &(Data['result_title'].str.contains(phrasedefault13_a3, na=False, case=False))
        )
    )
    &
     (
        (Data['result_title'].str.contains(phrasedefault13_a4, na=False, case=False))
        |
            (
                (Data['result_title'].str.contains(phrasedefault13_a5, na=False, case=False))
                &
                (
                    (Data['result_title'].str.contains(phrasedefault13_a6, na=False, case=False))
                    |
                    (
                        (Data['result_title'].str.contains(phrasedefault13_a7, na=False, case=False))
                        &(Data['result_title'].str.contains(phrasedefault13_a8, na=False, case=False))
                    )
                    |(Data['result_title'].str.contains(phrasedefault13_a9, na=False, case=False))
                    |
                    (
                        (Data['result_title'].str.contains(phrasedefault13_a10, na=False, case=False))
                        &(Data['result_title'].str.contains(phrasedefault13_a11, na=False, case=False))
                    )
                )
            )
     )
),"tempsdg13_a"] = "SDG13_0a"

print("Number of results = ", len(Data[(Data.tempsdg13_a == "SDG13_0a")])) 
```


```python
test=Data.loc[(Data.tempsdg13_a == "SDG13_0a"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13.b


```
 TS=
(
  (
    ("climat*" NEAR/5 ("strateg*" OR "policy" OR "policies" OR "plan" OR "planning" OR "plans" OR "management"¨OR "adaptation communication$"))
    OR "nationally determined contribution$"
    OR "green climate fund" OR "Least Developed Countries Fund" OR "LDCF" OR "Special Climate Change Fund" OR "SCCF" OR "adaptation fund" OR "adaptation financ*"
    OR
      (        
        ("capacity" OR "capabilit*"
        OR "educat*" OR "curriculum" OR "curricula" OR "teacher training" OR "climate literacy"
        OR "research" OR "knowledge" OR "skills" OR "tools" OR "competenc*" OR "expertise" OR "training"
        OR "awareness" OR "responsibilit*"
        OR "infrastructure$" OR "technolog*" OR "early warning system$"
        OR "communication" OR "collaboration" OR "cooperation" OR "co operation" OR "social network$" OR "information network$"
        OR "economic resources" OR "financial resources" OR "human resource$"
        OR (("institutional" OR "administrative" OR "policy" OR "governance") NEAR/5 ("structure$" OR "values" OR "practices" OR "arrangement$" OR "resources"))
        )
        AND
            (
              ("climat*" OR "global warming" OR "climatic change$" OR "sea level rise")
              NEAR/5
                  ("action$" OR "sustainab*" OR "mitigat*" OR "adapt*" OR "cope" OR "coping" OR "resilien*"
                  OR "early warning" OR "warning system$" OR "preparedness" OR "risk$" OR "vulnerab*"
                  OR "awareness" OR "climate education" OR "climate sensitive education" OR "climate change education" OR "climate literacy"
                  OR "solutions" OR "problems" OR "manag*"
                  )
            )
      )  
  )   
  AND
  (****LDCs and SIDS**** )
)
```
      


```python
# Term lists
termlist13_b1 = ["climate",
                 "klima"]
termlist13_b2 = ["strateg", "policy", "policies", "plan", "management", "adaptation communication",
                 "politikk", "retningslin", "ledelse", "leiing", "styring", "tilpasningskommunikasjon", "tilpassingskommunikasjon"]
termlist13_b3 = ["nationally determined contribution", "green climate fund", "least developed countries fund", "LDCF", "special climate change fund", "sccf", "adaptation fund",
                 "adaptation financ", 
                 "nasjonalt fastsatt bidrag", "nasjonalt fastsatte bidrag", "klimafond"]
termlist13_b4 = ["capacity", "capabilit", "educat", "curriculum", "curricula", "teacher training", "climate literacy", "research", "knowledge", "skills",
                 "tools", "competenc", "expertise", "training", "awareness", "responsibilit", "infrastructure", "technolog", "early warning system",
                 "communication", "collaboration", "cooperation", "co operation", "social network", "information network", 
                 "economic resources", "financial resources", "human resource",
                 
                 "kapasitet", "evne", "utdann", "opplær", "pensum", "læreplan", "fagplan", "emneplan", "studieplan", "lærerutdann", "lærarutdann", "klimakompetanse", "forskning", "forsking", "kunnskap", "ferdighet", "ferdigheit",
                 "verktøy", "kompetanse", "ekspertise", "bevisst", "medvett", "medvit", "ansvar", "infrastruktur", "teknolog", "tidlig varsling", "tidleg varsling", "varslingssystem"
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
            ( 
              (Data['result_title'].str.contains(phrasedefault13_b1, na=False, case=False))&
              (Data['result_title'].str.contains(phrasedefault13_b2, na=False, case=False))       
            ) 
          |
            (Data['result_title'].str.contains(phrasedefault13_b3, na=False, case=False))
        )
    |
        (
          (
            (Data['result_title'].str.contains(phrasedefault13_b4, na=False, case=False))
          |
            (
             (Data['result_title'].str.contains(phrasedefault13_b5, na=False, case=False))&
             (Data['result_title'].str.contains(phrasedefault13_b6, na=False, case=False))
            )
          )
          &
           (  
              (Data['result_title'].str.contains(phrasedefault13_b7, na=False, case=False))&
              (Data['result_title'].str.contains(phrasedefault13_b8, na=False, case=False))
           )      
        )  
    )
    &(Data['LDCSIDS']==True)
),"tempsdg13_b"] = "SDG13_b"

print("Number of results = ", len(Data[(Data.tempsdg13_b == "SDG13_b")]))
```


```python
test=Data.loc[(Data.tempsdg13_b == "SDG13_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 13 mentions


```
TS=
("SDG 13" OR "SDGs 13" OR "SDG13" OR "sustainable development goal$ 13"
OR ("sustainable development goal$" AND "goal 13")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 13")
  AND ("climate action")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 13")
    NEAR/15 ("climate")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
```
  



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
       (Data['result_title'].str.contains(phrasedefault13_1, na=False, case=False))|
     (
      (Data['result_title'].str.contains(phrasedefault13_2, na=False, case=False))&
      (Data['result_title'].str.contains(phrasedefault13_3, na=False, case=False))
      ) |
     (
         (Data['result_title'].str.contains(phrasedefault13_4, na=False, case=False))&
         (Data['result_title'].str.contains(phrasedefault13_5, na=False, case=False))
     )
     |
      (Data['result_title'].str.contains(phrasedefault13_6, na=False, case=False))
),"tempmentionsdg13"] = "SDG13"

print("Number of results = ", len(Data[(Data.tempmentionsdg13 == "SDG13")]))
```


```python
test=Data.loc[(Data.tempmentionsdg13 == "SDG13"), ("result_id", "result_title")]
test.iloc[5:10, ]
```

## SDG 14

Webpages about SDG targets from the UN Association of Norway were used to get target translations and to help with Norwegian terms (https://www.fn.no/om-fn/fns-baerekraftsmaal/livet-i-havet).

Have also used "Realfagstermer", a controlled vocabulary for English and Norwegian scientific terms from the University of Oslo and University of Bergen - https://app.uio.no/ub/emnesok/realfagstermer/search

A website with Norwegian and English names for international environmental agreements from the Norwegian Environment Agency was used to help translate international agreement/convention names (https://www.miljodirektoratet.no/regelverk/konvensjoner/; accessed 24/01/23)

### Marine terms

Used together with most (but not all) targets to try and limit the results to the marine environment. Done by creating a T/F column ("marine_terms") that can be combined with other searches. T = contains a word indicating it is about the marine environment. 

```
TS=
(
  "ocean$" OR "oceanogra*" OR "marine" OR "submarine" OR "seas"
  OR "seabed" OR "seafloor" OR "seamount$" OR "hydrothermal vent$" OR "cold seep$" OR "continental shelf" OR "continental shelves" OR "continental slope"
  OR "subtidal" OR "intertidal" OR "deep sea" OR "bathyal" OR "abyssal"
  OR "rocky shore$" OR "beach*" OR "salt marsh*" OR "mud flat$" OR "mudflat$" OR "*tidal flat" OR "*tidal flats"
  OR "estuar*" OR "fjord$"
  OR "sea ice"

  OR "sea life" OR "sealife"
  OR "mangrove$"
  OR "kelp bed$" OR "kelp forest$" OR "seagrass*"
  OR (("seaweed$" OR "macroalga*") NEAR/5 ("bed$" OR "assemblage$" OR "communit*"))
  OR "sponge ground$" OR "organic fall$"
  OR "reef" OR "reefs"

  OR "coastal habitat$" OR "coastal ecosystem$" OR "coastal dune$" OR "coastal wetland$"
  OR "coastal water$" OR "coastal current$" OR "tidal current$"
  OR "coastal communit*" OR "coastal zone management"
  OR 
    (
      ("coast*" OR "*tidal")
      AND
          ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$"
          OR "offshore" OR "fish*" OR "aquaculture" OR "shrimp" OR "shellfish"
          )
    )
  OR 
    ("sea"
      AND
          ("marsh*" OR "wetland$" OR "bay$" OR "gulf" OR "lagoon$"
          OR "offshore" OR "ship*"
          OR "fish*" OR "aquaculture" OR "shrimp" OR "shellfish"
          OR "*tidal" OR "pelagic"
          )
    )
  OR
    (
      ("harbour$" OR "harbor$" OR "port" OR "ports")
      AND ("sea" OR "coast*" OR "gulf" OR "ship*" OR "maritime")
    )
)

OR

SO =
(
  "marine*" OR "ocean*" OR "estuar*" OR "deep sea*"
  .....

```


```python
#Term lists

termlist14_marine1 = ["marine", "mariculture", "barents sea", "norwegian sea",
                     "seabed", "seafloor", "seamount", "hydrothermal vent", "cold seep", "continental shelf", "continental shelves", "continental slope", 
                     "subtidal", "intertidal", "deep sea", "bathyal", "abyssal",
                     "rocky shore", "beach", "salt marsh", "mud flat", "mudflat", "tidal flat",
                     "estuar", "fjord", 
                     "sea ice",
                     "sea life", "sealife", "mangrove$", "kelp bed", "kelp forest", "seagrass", "seaweed", "macroalga", 
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
                      "skipsfart"                      
                     ]
                     #Difficult because "Fjære"(NO) is also a local municipality
                     #"tidevann"(NO) will cover several other terms, like tidevannssonen
                     #"skipsfart"(NO) was added here as in Norwegian it is likely to be used in a marine context. In English, "ship" is combined with other terms.
                     #In Norwegian I have added "havbruk"(NO) as this is aquaculture specifically in the sea, and "havforsuring"(NO) (as "hav" is difficult to use alone). 
                     #Also relevant geographic areas (e.g. Skagerrak), but some will be found by "havet"(NO) below (e.g. Barentshavet).

termlist14_marine2 = ["ocean", "oceans", "oceanogra.*", "seas", 
                      "marin", "oseanografi.*", "hav", "havet", "verdenshav", "sjø", "sjøen", "tang", "tare"
                      ]
                      #"marin"(EN&NO), "tang" (NO), "tare"(NO) are added here instead of untruncated in termlist_marine1 because it is part of other words (e.g. marinate)

termlist14_marine3 = ["sea", "coast", "coastal", "tidal",
                      "sjø.*", "kyst.*", "tideva.*"
                      ]
                      #"tideva"(NO) covers both tidevatn and tidevann while excluding "tide"

termlist14_marine4 = ["habitat", "ecosystem", "dune", "wetland", "marsh", "bay", "lagoon", "gulf", "water", "current", "pelagi",
                     "fish", "shrimp", "shellfish", "aquacultur",
                      "harbour", "harbor", "port", "maritim", "ship",

                      "leveområd", "økosystem", "våtmark", "sumpmark", "viker", "bukter", "strøm",
                      "fisk", "akvakultur", 
                      "havn", "båt", "elvemunn"
                     ] 
                     #In the original string, "sea" and "coast" etc. were combined with this set to remove noise (i.e. coastal cities)
                     #However, in a title search, I think we lose more relevant than we get noise, so I do not combine with this set.
                        #"elvemunn"(NO) is moved here as used with rivers into lakes also
                        #"maritim", "pelagi" cover both the Norwegian and English terms
                        #"bay" and "ship" are potentially problematic with free truncation, but combined with the terms in marine3 don't seem to cause issues

termlist14_marine5 = ["marine", "ocean", "oceans", "oceanogra.*", "estuar.*", "deep sea", "sea", 
                      "havforsk.*", "havbruk.*"
                      ] 
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

```
TS=
(
  ("pollut*"
  OR "wastewater" OR "waste water" OR "sewage" OR "sewer$"
  OR "eutrophicat*" OR "excess nutrient$" OR "excessive nutrient$"
  OR "effluent$" OR "nutrient runoff" OR "nutrient run off"
  OR
    (
      ("aquaculture" OR "farm*" OR "industr*" OR "livestock" OR "agricultur*" OR "household$" OR "domestic" OR "urban" OR "radioactive")
      NEAR/15 ("waste" OR "discharge" OR "runoff" OR "run off")          
    )
  OR "litter" OR "littering" OR "garbage patch"
  OR ("debris" NEAR/5 ("coastal" OR "marine" OR "ocean*"))
  OR "microplastic$" OR "micro plastic$" OR "nanoplastic$" OR "nano plastic$" OR "plastic waste" OR ("plastic$" NEAR/3 ("problem" OR "debris"))
  OR
    (
      ("heavy metal$" OR "toxic metal$" OR "mercury" OR "arsenic" OR "cadmium" OR "chromium" OR "copper" OR "nickel" 
      OR "organotin$" OR "tributyltin" OR "TBT" OR "mining" OR "mine tailing$" OR "oil"
      )
      NEAR/15 ("contamination" OR "contaminated")   
    )
  OR
    (
      (("cd" OR "ch" OR "cu" OR "ni" OR "pb" OR "hg") NEAR/15 ("contamination" OR "contaminated")) 
      AND ("arsenic" OR "cadmium" OR "chromium" OR "copper" OR "nickel" OR "lead" OR "mercury")
    )
  OR "contaminant$" OR "bioaccumula*" OR "bioconcentrat*" OR "ecotox*" OR "toxic chemical$"
  OR "endocrine disrupting chemical$"
  OR "persistent organic pollutant$" OR "pesticide$" OR "herbicide$" OR "polychlorinated biphenyl$" OR "PCB" OR "DDT" OR "hexachlorocyclohexane" OR "hexachlorobenzene" OR "hexachlorobutadiene" OR "pentachlorobenzene" OR "pentachlorophenol" OR "pentachloroanisole" OR "hexabromocyclododecane" OR "polybrominated diphenyl ether$" OR "perflurochemicals" OR "PFAS" OR "endosulfan"
  OR "polycyclic aromatic hydrocarbon$" OR "PAH"
  OR "oil spill$"
  )
  NOT ("PM2.5" OR "PM10" OR "leaf litter")
)

```


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
                 "oljesøl", "oljeutslipp"
                 ]
                 #Can add "wastewater","waste water" back again if "waste" is too general alone
                 #"pesticid" will find Norwegian-ifications of this word.
                 #"avfall" (NO), after testing, is ok to use alone, thus the specific terms are commented out above.

termlist14_1b = ["PCB","DDT","PAH"] #can be searched for with case sensitive

termlist14_1c = ["litter", 
                 "bly", "arsen", "krom", "tinn", "plast"
                 ]
                 #"Litter" needs specific truncation because it is part of "litteratur" in Norwegian
                 #These Norwegian heavy metals are short words and need to prevent truncation

termlist14_1d = ["oil", "lead",
                 "olje", "kjemikal.*"]

termlist14_1e = ["contamina", "toksis"]

termlist14_1not = ["PM2.5","PM10","leaf litter"] 

phrasedefault14_1a = r'(?:{})'.format('|'.join(termlist14_1a))
phrasedefault14_1b = r'(?:{})'.format('|'.join(termlist14_1b))
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
            | (Data['result_title'].str.contains(phrasedefault14_1b, na=False, case=True)) #case = True
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

#### Phrase 1

```
TS=
(
  "LSMPA$" OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
  OR "particularly sensitive sea area$"
  OR
    (
      ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving")
      NEAR/3 ("area$" OR "zone$" OR "habitat$" OR "ecosystem$")
    )
   OR ("no-take" NEAR/3 ("area$" OR "zone*" OR "reserve$")) OR "NTMR$"
   OR "marine spatial planning" OR "spatial management"
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
```


```python
#Termlists
termlist14_2a = ["marine reserve", "ocean reserve", "marine nature reserve", "marine park", "particularly sensitive sea area",
                 "marine spatial planning",
                 "coastal zone management","integrated coastal zone planning","coastal resources management",
                 "locally managed marine area",

                 "marint vernområde","marine vernområde","marine verneområde","marine reservat",
                 "integrert kystsone", "kystplanlegging", "kystsoneforvaltning"
              ]
termlist_142acaps = ["LMMA","NTMR","ICZM","LSMPA"] #can search case sensitive

              #Above I have the terms that are specific to the marine environment
              #In the rest of the term lists, the terms need combining with marine terms

termlist14_2b = ["spatial management", "community based management","resilience based management",
                 "herbivore management area", 
                 "ecosystem-based", "area-based manag", "area-based approach",
                 "sustainable management", "sustainable governance",
                 "no-take area", "no-take zone", "no-take reserve",

                 "naturreservat", "biotopvernområde", "nasjonalpark", "bevarte område", "bevart område", "bevaringsområde",
                 "økosystembasert forvaltning", "økosystemtilnærming", "økosystembasert styring", "forvaltningsplaner",
                 "samfunnsforvalt", "bærekraftig forvalt", "berekraftig forvalt", "arealforvalt", "bærekraftig ledelse", "berekraftig leiing",
                 "fiskeforbud", "fiskevernsone"
                ]

termlist14_2c = ["protect","conserve","conservation","conserves","conserving",
                "vernet", "verne", "verna", "vern av", "bevare", "bevaring", "frede", "freda", "fredning", "beskytt" 
                ]

termlist14_2d = ["area", "zone", "habitat","ecosystem",
                "område", "sone", "miljø", "leveområd", "økosystem"
                ]

phrasedefault14_2a = r'(?:{})'.format('|'.join(termlist14_2a))
phrasedefault14_2acaps = r'(?:{})'.format('|'.join(termlist_142acaps))
phrasedefault14_2b = r'(?:{})'.format('|'.join(termlist14_2b))
phrasedefault14_2c = r'(?:{})'.format('|'.join(termlist14_2c))
phrasedefault14_2d = r'(?:{})'.format('|'.join(termlist14_2d))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_2a, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasedefault14_2acaps, na=False, case=True)) #case = True
        | (Data['result_title'].str.contains(phrasedefault14_2b, na=False, case=False))
        | ((Data['result_title'].str.contains(phrasedefault14_2c, na=False, case=False)) & (Data['result_title'].str.contains(phrasedefault14_2d, na=False, case=False)))
    )
    &(Data['marine_terms']==True)
),"tempsdg14_02"] = "SDG14_02"

print("Number of results = ", len(Data.loc[(Data.tempsdg14_02 == "SDG14_02")]))  
```

#### Phrase 2

```
TS=
(
  ("manage" OR "managing" OR "managed" OR "conserve" OR "conserving" OR "protect" OR "protecting" OR "protected" OR "restore" OR "restoring"
  OR "management" OR "conservation" OR "protection" OR "restoration"
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


```python
#Termlists
termlist14_2e = ["manag", "conserv", "protect", "restor",
                 "forvalt", "verne", "verna", "vern av", "miljøvern","bevare", "bevaring", "frede", "freda", "fredning", "beskytt", "gjenoppbygg", "restaurer", 
                 "bærekraftig bruk", "berekraftig bruk"
                 ]
                 #"vernet"(NO) will also find "vernetiltak"

termlist14_2f = ["habitat","ecosystem","communit",
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
                "naturmangfoldloven", "områdevern", "artsforvaltning"
                ]
                #added Norwegian-specific legislation

termlist14_2g = ["tare.*", "tang", "tangart.*"
                 ]
                 #Norwegian terms from 2f that need prevent truncation

termlist14_2h = ["BBNJ", "CBD", "HELCOM", "OSPAR", "UNEP", "CCAMLR"]

phrasedefault14_2e = r'(?:{})'.format('|'.join(termlist14_2e))
phrasedefault14_2f = r'(?:{})'.format('|'.join(termlist14_2f))
phrasespecific14_2g = r'\b(?:{})\b'.format('|'.join(termlist14_2g))
phrasedefault14_2h = r'(?:{})'.format('|'.join(termlist14_2h))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_2h, na=False, case=True)) 
        | ((Data['result_title'].str.contains(phrasedefault14_2e, na=False, case= False)) & (Data['result_title'].str.contains(phrasedefault14_2f, na=False, case=False)))
        | ((Data['result_title'].str.contains(phrasedefault14_2e, na=False, case= False)) & (Data['result_title'].str.contains(phrasespecific14_2g, na=False, case=False)))
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

```
TS =
(
  (
    ("impact*" OR "effect$" OR "affect$" OR "response$" OR "consequence$"
    OR "results in" OR "changes" OR "alter*"
    OR "sensitiv*" OR "vulnerab*" OR "threat*"
    OR "resilience" OR "adaptive capacity" OR "coping" OR "toleranc*"
    OR "calcif*" OR "decalcif*" OR "calcium carbonate"
    OR "aragonite" OR "calcite" OR "carbonate saturation"
    OR "extinction$" OR "adaptation" OR "adaptive capacity"
    OR "competition" OR "recruitment" OR "survival" OR "reproduction"
    )
    NEAR/15
        ("acidi*" OR "OA" OR "ocean ph" OR "seawater ph"
        OR "low ph" OR "declining ph" OR "decreas* ph" OR "effect$ of ph"
        )
  )
  AND "ocean$"
)
```

Compared to the original string, we have added the term "monitoring" ("overvåk"). This is somewhat of an expansion; the original string was very limited to terms to do with impacts. If one can consider monitoring as a way of "addressing" impacts then it should be added to the original string too. 


```python
#Termlists
termlist14_3a = ["impact", "effect", "affect", "respons", "consequence",
                 "results in", "changes", "alters", "altering", "changing",
                 "sensitiv", "vulnerab", "threat",
                 "resilien", "coping", "toleran",
                 "calcif", "carbonate", "aragonit", "calcite", 
                 "extinct", "adapt", "competiti", "recruit", "surviv", "reproduc",
                 "monitor"

                 "påvirk", "impakt", "konsekvens", "effekt",
                 "resultat", "endring", 
                 "sårbar", "truet", "truer", " trua", " trued", "stress", "tåle", 
                 "forkalk", "karbonsyre", "karbonat", "kalsit", "skjell", #"aragonit", 
                 "utrydd", "tilpass", "konkurr", "rekrutter", "overleve", "formering", "reproduksjon",
                 "overvåk", "overvak"
                ]
                #spaces added with "trua"(NO) and "trued"(NO) on purpose to avoid truncation

termlist14_3b = ["acidi", "ocean ph", "seawater ph", "low ph", "declining ph", "decreasing ph", "decreased ph", "effect of ph", "effects of ph",
                 
                 "forsur", "nedgangen i pH", "nedgang i ph", "lav ph", "lavere ph", "lågere ph", "surere hav", "surare hav", "surt hav"
                ]

termlist14_3c = ["OA"]

phrasedefault14_3a = r'(?:{})'.format('|'.join(termlist14_3a))
phrasedefault14_3b = r'(?:{})'.format('|'.join(termlist14_3b))
phrasespecific14_3c = r'\b(?:{})\b'.format('|'.join(termlist14_3c))
```


```python
#Search 1

#Note that "havforsuring" (NO; ocean acidification) is included in the marine terms, so it should not be a problem to find works using this term even when combined with marine terms.

Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_3a, na=False, case=False)) 
        & (
            (Data['result_title'].str.contains(phrasedefault14_3b, na=False, case=False)) 
            | (Data['result_title'].str.contains(phrasespecific14_3c, na=False, case=True))
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

#### Phrase 1
```
TS=
(     "overfish*"
      OR "bycatch" OR "by-catch"
      OR "IUU fishing"
      OR (("gear" OR "nets") NEAR/5 ("abandoned" OR "lost" OR "discarded"))
      OR "ghost fishing" OR "ghost nets" OR "ALDFG" OR "poison fishing"
      OR
        (
          ("overharvest*" OR "overexploit*" OR "overcapacity" OR "collaps*" OR "closure$"
          OR "illegal*" OR "unreport*" OR "unregulated" OR "corruption" OR "destructive" OR "blast" OR "dynamite" OR "cyanide"
          )
          NEAR/15 ("fishing" OR "fisher*" OR "shellfish*" OR "trawl*")
        )
      OR ("trawl*" NEAR/15 ("degrad*" OR "damag*"))    
)
```


```python
#Termlists
termlist14_4a = ["overfish", "bycatch", "by-catch", "IUU fish", 
                 "ghost fishing", "ghost net", "ALDFG", "poison fishing",

                 "overfisk", "ulovlig fisk", "ulovlige fisk", "ulovleg fisk", "ulovlege fisk", "tjuvfiske", "bifangst", "UUU fiske", "UUU-fiske",
                 "spøkelsesfiske", "tapte garn"
                ]

termlist14_4b = ["gear", "net", "nets",
                 "fiskeredskap.*", "fiskegarn", "havteine.*", "torskebur", "teina"
                ]
termlist14_4c = ["abandoned", "lost", "discarded",
                 "tapt", "mistet", 
                ]

termlist14_4d = ["trawl", "trawling",
                 "trål", "bunntrål.*", "trålfiske"
                 ]
                 #"Trål" (NO) causes problems alone with free truncation (e.g. stråle)
termlist14_4e = ["degrad", "damag", "harm",
                 "skade", "ødelag", "ødeleg"
                ]

termlist14_4f = ["overharvest", "overexploit", "overcapacit", "collaps", "closure",
                 "illegal", "unreport", "unregulat", "corrupt", "destruct", "blast", "dynamite", "cyanid",
                 "overbeskat", "kollaps", "stenge", "stenging",
                 "ulovlig", "ulovleg", "urapport", "uregulert", "korrupsj", "ødelegg", "ødelagt", "forring", "dynamitt", "eksplosiv", "tapt redskap", "tapte redskap"
                ]
                #"cyanid" covers norwegian and english
termlist14_4g = ["fishing", "fisher", "shellfish", "trawl",                
                 "fiske", "skalldyr"                 
                ]
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

#### Phrase 2

Fish species taken from The Norwegian Directorate of Fisheries https://www.fiskeridir.no/Yrkesfiske/Tall-og-analyse/Fangst-og-kvoter/Fangst/Fangst-fordelt-paa-art 
```
TS=
(
  ("manag*" OR "plan" OR "planning" OR "governance"
  OR "restor*" OR "stock recovery"
  OR "sustainab*"
  OR "EBFM" OR "ecosystem approach*"
  OR "maximum sustainable yield*" OR "MSY"
  OR "marine stewardship council"
  OR "regional fisheries management organi?ation$" OR "RFMOs"
  OR "UNCLOS" OR "convention on the law of the sea"
  OR "fish stocks agreement"
  OR "code of conduct for responsible fisheries" OR "CCRF"
  OR "port state measures agreement"
  OR "UNFSA" OR "Management of Straddling Fish Stocks" OR "Management of Highly Migratory Fish Stocks"
  OR "deep-sea fisheries guidelines" OR "Management of Deep-sea Fisheries in the High Seas"
  OR "common fisheries policy"
  OR "law$" OR "legislation" OR "instrument$" OR "strateg*" OR "policy" OR "policies" OR "framework" OR "agreement*" OR "treaty" OR "treaties"
  )
  NEAR/15
      ("fishery" OR "fisheries" OR "fishing"
      OR (("harvest*") NEAR/15 ("fish*" OR "shellfish*"))
      OR "fish stock$" OR "overfishing"
      OR ("catch" NEAR/3 ("entitlement" OR "limit$" OR "tolerance$"))
      )
)
```


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
                 "politikk", "lovverk", "regelverk", "regler", "rettningslin", "utredning", "utgreiing", "rammeverk", "avtale", "forskrift"
                ]
termlist14_4i = ["EBFM", "MSY", "RFMO", "UNCLOS", "CCRF", "UNFSA"]
                #terms that need case-sensitive search
termlist14_4j = ["law", "plan", "plans",
                 "lov", "planer"
                ]
                #terms that need prevented truncation
termlist14_4k = ["fish", "cod stock", "cod population", "herring", "saithe", "haddock", "mackrel", "capelin", "blue whiting", #"fishing", "fisher", "shellfish", "fish stock", "overfish",                
                 "fiske", "skalldyr", "torsk", "skrei", "kysttorsk", "sild", "sei ", "seifisk", "hyse", "makrell", "lodde ", "loddefisk", "kolmule"
                ]
                #terms where I prevent left truncation ("orthograFISKE"). 
                #Here we have added some Norwegian fish species, taken from the Norwegian Directorate of Fisheries ("utvalgte art")
                #"sei"(NO) was however difficult to include alone, have added a space after to prevent truncation in both direction
termlist14_4l = ["catch",
                 "fangst"  
                ]
termlist14_4m = ["entitlement", "limit", "tolerance",
                 "begrens", "kvote"              
                ]                                
phrasedefault14_4h = r'(?:{})'.format('|'.join(termlist14_4h))
phrasedefault14_4i = r'(?:{})'.format('|'.join(termlist14_4i))
phrasespecific14_4j = r'\b(?:{})\b'.format('|'.join(termlist14_4j))
phrasespecific14_4k = r'\b(?:{})'.format('|'.join(termlist14_4k))
phrasedefault14_4l = r'(?:{})'.format('|'.join(termlist14_4l))
phrasedefault14_4m = r'(?:{})'.format('|'.join(termlist14_4m))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault14_4h, na=False, case=False)) 
        | (Data['result_title'].str.contains(phrasedefault14_4i, na=False, case=True)) #case = True
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


```
TS=
(
  "MPA" OR "MPAs" OR "LSMPA$" OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
  OR "particularly sensitive sea area$"
  OR
    (
      ("protect*" OR "conserved" OR "conservation" OR "conserves" OR "conserving")
      NEAR/3 ("area$" OR "zone$" OR "habitat$" OR "ecosystem$")
    )
  OR ("no-take" NEAR/3 ("area$" OR "zone*" OR "reserve$")) OR "NTMR$"
)
```


```python
#Termlists
termlist14_5a = ["marine reserve", "ocean reserve", "marine nature reserve", "marine park", "particularly sensitive sea area",
                 "nature reserve","national park",
                 "no-take area", "no-take zone", "no-take reserve",

                 "vernområde","vernområde", "vernet økosystem", "marine reservat",
                 "naturreservat", "nasjonalpark", "biotopvernområde", "biosfæreområde", "bevarte område", "bevaringsområde","fredningsområde","nasjonalpark",
                 "fiskeforbud" 
                 ]
termlist_145acaps = ["MPA","LSMPA","NMTR"] #can search case sensitive

termlist14_5b = ["protect","conserved","conservation","conserves","conserving",
                "verne", "verna", "vern av","bevare","bevaring","frede","freda","fredning","beskytt"
                ]

termlist14_5c = ["area","zone", "habitat", "ecosystem",
                "område", "sone", "leveområd", "miljø", "økosystem"
                ]

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

Phrases 1 and 2:
```
TS =
(
  ("subsid*"
    NEAR/15
        ("fishing" OR "fisher*" OR "overfishing" OR "bycatch" OR "trawling"
        OR (("harvest*" OR "overcapacity") NEAR/15 ("fish*" OR "shellfish*"))
        )  
  )
  NOT ("larval subsidi*" OR "recruitment subsidi*")
)

TS=
(
  ("ODA" OR "official development assistance" OR "doha development agenda" OR "hong kong ministerial" OR "world trade organization" OR "WTO")
  NEAR/15
      ("fishing" OR "fisher*" OR "overfishing"
      OR (("harvest*" OR "overcapacity") NEAR/15 ("fish*" OR "shellfish*"))
      )  
)
```


```python
#Termlists
termlist14_6a = ["subsid","official development assistance","doha development agenda","hong kong ministerial","world trade organization",
                "statsstøtte", "offentlig støtte", "utviklingsstøtte", "bistand", "Verdens handelsorganisasjon", "Doha-runden", "ministermøtet i Hongkong"
                 ]
                 #"subsid" will find both the Norwegian and English
termlist14_6acaps = ["ODA", "WTO"]

termlist14_6b = ["fishing", "fisher", "shellfish", "trawl",                
                 "fiske", "skalldyr"
                ]
                #"fishing" will find overfishing

#termlist14_6not = ["larval subsid", "recruitment subsid"] 
#Doesn't seem to be needed here in a title search

phrasedefault14_6a = r'(?:{})'.format('|'.join(termlist14_6a))
phrasedefault14_6acaps = r'(?:{})'.format('|'.join(termlist14_6acaps))
phrasedefault14_6b = r'(?:{})'.format('|'.join(termlist14_6b))
#phrasedefault14_6not = r'(?:{})'.format('|'.join(termlist14_6not))
```


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault14_6a, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault14_6acaps, na=False, case=True)))
    & (Data['result_title'].str.contains(phrasedefault14_6b, na=False, case=False))
),"tempsdg14_06"] = "SDG14_06"

print("Number of results = ", len(Data[(Data.tempsdg14_06 == "SDG14_06")])) 
```


```python
test=Data.loc[(Data.tempsdg14_06 == "SDG14_06"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 14.7

*14.7 By 2030, increase the economic benefits to small island developing States and least developed countries from the sustainable use of marine resources, including through sustainable management of fisheries, aquaculture and tourism*

*Innen 2030 sikre at de økonomiske fordelene ved bærekraftig bruk av havets ressurser, blant annet gjennom bærekraftig forvaltning av fiskeri, akvakultur og turistnæring, i større grad kommer små utviklingsøystater og de minst utviklede landene til gode*

```
TS =
(
    ("econom*" OR "GDP" OR "wealth"
    OR "exploit*" OR "goods and services" OR "ecosystem service$"
    OR "socio economic" OR "socioeconomic"
    OR "livelihood$" OR "job$" OR "income$" OR "profit*"
    OR "trade" OR "trading" OR "market$"
    OR "monetary" OR "moneti*" OR "investor$"
    OR "bio-econom*" OR "bioeconom*"            
    OR "blue growth" OR "blue econom*" OR "blue bond$"
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
      (****SIDS and LDCs****
      )
)

```


```python
#Termlists
termlist14_7a = ["econom","wealth",
                 "exploit","goods and services","ecosystem service",
                 "livelihood","job","income","profit","trade","trading","market",
                 "monetary","moneti","investor",
                 "blue growth","blue bond",

                 "økonomi", "rikdom",
                 "utnytt", "varer", "tjenester",
                 "levebrød", "jobb", "arbeid", "inntekt", "handel", "marked", "markad",
                 "penger",
                 "blå vekst", "blåvekst"
                 ]
                 #"Blue/Bio economy" and "socioeconomic" (NO: blå/bio økonomi, sosioøkonomisk) is covered by "econom" (NO: økonomi)

termlist14_7acaps = ["GDP"] #can search case sensitive

termlist14_7b = ["sustainab",  
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

                 "bærekraft","berekraft",
                 "økosystem tilnærming", "økosystembasert forvaltning", "økosystembasert styring", "forvaltningsplaner",
                 "integrert kystsone", "kystplanlegging", "kystsoneforvalt",
                 "samfunnsforvalt", "bærekraftig forvalt", "berekraftig forvalt", "arealforvalt",
                 "marint vernområde","marine vernområde","marine verneområde","marine reservat",
                 "naturreservat", "biotopvernområde", "nasjonalpark", 
                 "bevarte område", "bevaringsområde", "fredet område", "vernet område", "marine vernområde", "marine verneområde",
                 #if this term list is used in the search, the agreement translations need to be added from 14.2c here. Currently it is not used (see note below)
                 "fiskeriforvalt", "fiskeriplanlegg", 
                 "likevektsfangst"
                ]

termlist14_7bcaps = ["LMMA","ICZM","MPA","RFMO","CCRF","UNFSA"] 

phrasedefault14_7a = r'(?:{})'.format('|'.join(termlist14_7a))
phrasedefault14_7acaps = r'(?:{})'.format('|'.join(termlist14_7acaps))
phrasedefault14_7b = r'(?:{})'.format('|'.join(termlist14_7b))
phrasedefault14_7bcaps = r'(?:{})'.format('|'.join(termlist14_7bcaps))
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

```
TS= ("transfer of marine technolog*" OR "marine technology transfer")
```


```python
#Termlists
termlist14_aa = ["transfer of marine technolog", "marine technology transfer", "technology transfer",
                 "teknologioverføring", "overføring av marin teknologi", "overføre marin teknologi", "overføre teknologi" 
                 ]
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
```
TS=
(
      ("establish*" OR "build*" OR "develop*" OR "implement*" OR "propos*" OR "design" OR "provide" OR "provision"
      OR "increas*" OR "improv*" OR "strengthen*" OR "enhanc*" OR "upgrad*" OR "accelerat*" OR "prioriti*" OR "promot*" OR "enabl*"
      OR "cooperat*" OR "co-operat*" OR "collaborat*" OR "network$" OR "partnership$"
      OR "open data" OR "data sharing" OR "open science"
      OR(
          ("knowledge" OR "technolog*" OR "technical" OR "research" OR "scientific" OR "R&D")
          NEAR/3 ("transfer" OR "sharing" OR "shared" OR "share" OR "cooperat*" OR "co-operat*" OR "collaborat*" OR "partnership$")
        )
      OR "invest" OR "investing" OR "fund" OR "funding" OR "financing" OR "financial support" OR "financial resources"
      OR (("economic" OR "financial*" OR "monetary") NEAR/3 ("support*" OR "assist*" OR "aid"))
      OR "ODA" OR "cooperation fund$"
      OR(
          ("international" OR "foreign" OR "development")
          NEAR/3 ("aid" OR "assistance" OR "fund$" OR "funding" OR "financing" OR "finance" OR "grant$" OR "investment$" OR "network$")
        )
      OR "plan" OR "planned" OR "planning"
      OR "policy" OR "policies" OR "initiative$" OR "framework" OR "governance" OR "strategy" OR "programme$" OR "agenda"
      OR "innovation"
      )
      NEAR/5
          ("taxonomic research" OR "genetic research" OR "biodiversity research" OR "diversity research" OR "taxonomic science" OR "fisheries science"
          OR "citizen science"
          OR (("ocean" OR "marine") NEAR/1 ("research" OR "science"))
          OR
            (
              ("research" OR "scientific" OR "science" OR "technology" OR "biotech*"
              OR "taxonom*" OR "genetic" OR "species" OR "biodiversity" OR "diversity"
              )
              NEAR/5
                  ("knowledge" OR "capacity" OR "advisor*"
                  OR "capabilit*" OR "training"  OR "expertise" OR "skills" OR "compentenc*"
                  OR "infrastructure" OR "facilities" OR "research vessel$" OR "vehicle$" OR "laboratories" OR "equipment" OR "herbaria" OR "museum collection$"
                  OR "database$" OR "software" OR "data" OR "register$" OR "reference librar*" OR "inventory" OR "inventories" OR "information system$"
                  OR "guidelines"
                  OR "investment$" OR "funding" OR "GERD" OR "expenditure"
                  OR "network$" OR "sharing" OR "joint research" OR "joint effort$" OR "collaborat*" OR "international cooperation"
                  )
            )
          OR "data infrastructure$" OR "data network$" OR "ocean big data" OR "smart ocean" OR "modelling technique$"
          OR "observ* network$" OR "observ* system$" OR "observ* facilities" OR "monitoring network$" OR "biomonitoring"
          OR "remote sensing equipment" OR "tide gauges"
          OR
            (
              ("ocean*" OR "marine" OR "biological" OR "ecological" OR "biodiversity" OR "environmental")
              NEAR/3 ("observator*" OR "monitoring")
            )
          )
)
```


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
                 "innovasjon"
                 ] 
                 #several words work in both languages (e.g. "promot", "design", "assist", "strateg")            
                 
termlist14_ac = ["plan","planned","planning","aid","ODA",
                 "øke", "øker", "midler"
                 ] #Control truncation

termlist14_ad = ["knowledge","technolog","technical","research","scientific","R&D",
                 "kunnskap", "teknologi", "teknisk", "forskning", "vitenskap", "innovasjon"]
termlist14_ae = ["sharing","shared","share","cooperat","co-operat","collaborat","partnership","network",
                 "deling", "samarbeid", "partnerskap", "nettverk"]

termlist14_af = ["research", "science", "scientific", "biotech", "ocean technolog",
                 "data infrastructure","data network","big data","smart ocean","modelling technique",
                 "biomonitoring","remote sensing equipment","tide gauge",

                 "forskning", "vitenskap", "bioteknol", "havteknolog", "marin teknolog",
                 "data infrastruktur", "datanettverk", "stordata", "smart hav", "modellering",
                 "miljøovervåk", "miljøovervak", "fjernmålingsutstyr"
                 ]
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
                 "nettverk", "deling", "samarbeid"
                 ]

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
```
TS=
(
  (
    (("blue growth" OR "blue econom*" OR "marine economy") AND "sustainab*")
    OR
    (
      ("bioresource$" OR "biological resource$" OR "genetic resource$" OR "living marine resources"
      OR "biodivers*" OR "biological diversity" OR "BBNJ" OR "species diversity" OR "genetic diversity" OR "genomic diversity" OR "taxonomic diversity"
      )
      AND
          ("bioprospect*" OR "biopiracy" OR "Nagoya protocol" OR "biotech*" OR "marine natural product$" ("bioactive$" NEAR/3 ("compound*" OR "substance*"))
          OR "bio-econom*" OR "bioeconom*" OR "blue growth" OR "blue econom*" OR "blue bond$" OR "marine economy"
          )
    )
    OR
    (
      ("biodivers*" OR "biological diversity" OR "species diversity" OR "genetic diversity" OR "genomic diversity" OR "taxonomic diversity")
      NEAR/5
          ("benefit$"
          OR "sustainable development" OR "development intervention$" OR "human development" OR "social development" OR "*economic development"
          OR "tourism" OR "ecotourism" OR "tourist$" OR "sightsee*"
          OR "fisher*" OR "fishing" OR "aquaculture" OR "fish farm*" OR "harvest*" OR "aquarium trade"
          OR "exploit*" OR "goods and services" OR "ecosystem service$"
          OR "social ecological" OR "socialecological" OR "socioecological" OR "socio economic" OR "socioeconomic"
          OR "econom*" OR "GDP" OR "wealth" OR "monetary" OR "moneti*" OR "investor$"
          OR "livelihood$" OR "job$" OR "income$" OR "profit*"
          OR "trade" OR "trading" OR "market$"
          OR ("sustainab*" NEAR/5 ("utilization" OR "use" OR "using" OR "usage"))
          )
    )
    OR
    (
      ("bioresource$" OR "biological resource$" OR "genetic resource$" OR "living marine resources")
      NEAR/15
          ("benefit$"
          OR "sustainable development" OR "development intervention$" OR "human development" OR "social development" OR "*economic development"
          OR "tourism" OR "ecotourism" OR "tourist$" OR "sightsee*"
          OR "fisher*" OR "fishing" OR "aquaculture" OR "fish farm*" OR "harvest*" OR "aquarium trade"
          OR "exploit*" OR "goods and services" OR "ecosystem service$"
          OR "social ecological" OR "socialecological" OR "socioecological" OR "socio economic" OR "socioeconomic"
          OR "econom*" OR "GDP" OR "wealth" OR "monetary" OR "moneti*" OR "investor$"
          OR "livelihood$" OR "job$" OR "income$" OR "profit*"
          OR "trade" OR "trading" OR "market$"
          OR ("sustainab*" NEAR/5 ("utilization" OR "use" OR "using" OR "usage"))
          )
    )
  )
  AND
    (****LMICs****
    )
) 
```


```python
#Termlists
termlist14_ak = ["blue growth","blue econom","marine economy",
                 "blå vekst", "blåvekst", "blå økonomi", "marin økonomi"]                   
termlist14_al = ["sustainab",
                 "bærekraft", "berekraft"] 

termlist14_am = ["bioresource","biological resource","genetic resource","living marine resources",
                 "biodivers","biological diversity","BBNJ","species diversity","genetic diversity","genomic diversity","taxonomic diversity",

                 "bioressurs", "biologiske ressurs", "genressurs", "genetiske ressurs", "levende marine ressurs",
                 "biologisk diversit", "biologisk mangfold", "biologisk mangfald", "artsmangfold", "artsmangfald", "genetisk mangfold", "genetisk mangfald", "taksonomisk mang", "naturmangfold", "naturmangfald"                 
                 ]
termlist14_an = ["bioprospect","biopiracy","Nagoya","biotech","marine natural product","bioactive",
                 "bio-econom","bioeconom","blue growth","blue econom","blue bond","marine economy",
                 "benefit","sustainable development","development intervention","human development","social development","economic development",
                 "tourism","tourist","sightsee",
                 "fisher","fishing","aquaculture","fish farm","harvest","aquarium trade",
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
                 "bærekraftig bruk", "berekraftig bruk",  "selvbærende", "sjølvberande", "miljøvennlig", "miljøvennleg", "miljøvenleg", "miljøbevisst"
                 ]

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

Phrase 1 & phrase 2
```
TS =
(
  ("access*" OR "right$"
  OR "commons" OR "common property" OR "common fishing ground$" OR "ownership" OR "inheritance"
  OR "conflict$" OR "dispute$" OR "contested" OR "competition"
  OR "inequitab*" OR "marginali*" OR "criminali*" OR "appropriation$"
  OR "blue injustice" OR "blue justice" OR "distributional justice"
  )
  AND
      ("traditional fishing"
      OR
        (
          ("fisher*" OR "fishing" OR "shellfish" OR "marine resource$" OR "marine harvest*")
          NEAR/5 ("small-scale" OR "artisan*" OR "subsistence" OR "indigenous")    
        )
      )
)

TS =
(
  ("governance" OR "planning" OR "legislation" OR "policy" OR "policies" OR "framework" OR "strateg*" OR "legislat*" OR "law" OR "laws" OR "regulations")
  NEAR/5
    ("traditional fishing"
    OR
      (
        ("fisher*" OR "fishing" OR "shellfish" OR "marine resource$" OR "marine harvest*")
        NEAR/5 ("small-scale" OR "artisan*" OR "subsistence" OR "indigenous")    
      )
    )
)


```


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
                 "styring", "ledelse", "leiing", "politikk", "retningslinj", "rammverk", "planlegging", "regulativ", "lovgiv", "forskrift",
                ]
                #"rett" covers both rights and justice (rett, rettferd)

termlist14_bb = ["law", "laws",
                 "lov", "lovverk", "arv"] #terms to control truncation

termlist14_bc = ["fishing", "fisher", "fish market", "shellfish", "marine resource", "marine harvest",                
                 "fiske", "skalldyr", "marine ressurs", "havbruk"
                ]

termlist14_bd = ["traditional fishing","small-scale", "artisan", "subsistence", "indigenous", "sami", "sapmi", 
                 "tradisjonel", "småskala", "subsistens", "levebrød", "urfolk", "urbefolk", "samene"
                ]

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


#### Phrase 1
```
TS =
(
  "law of the sea" OR "UNCLOS"
  OR "the future we want"
  OR (("biodivers*" OR "biological diversity" OR "fish*") NEAR/3 ("beyond national jurisdiction" OR "ABNJ"))
  OR "BBNJ"
  OR "common fisheries policy"
  OR "marine stewardship council"
  OR "regional fisheries management organi?ation$" OR "RFMOs"
  OR "fish stocks agreement"
  OR "code of conduct for responsible fisheries" OR "CCRF"
  OR "port state measures agreement"
  OR "UNFSA" OR "Management of Straddling Fish Stocks" OR "Management of Highly Migratory Fish Stocks"
  OR "deep-sea fisheries guidelines" OR "Management of Deep-sea Fisheries in the High Seas"
  OR ("directive$" NEAR/3 "marine spatial planning")
  OR "habitats directive" OR "convention on biological diversity"
  OR "Convention on International Trade in Endangered Species"
  OR "Regional seas programme"
  OR "Water framework directive"
  OR "OSPAR convention"
  OR "Marine strategy framework directive" OR "MSFD"
  OR "Barcelona convention"
  OR "Global Programme of Action for the Protection of the Marine Environment"
  OR "MARPOL" OR "prevention of pollution from ships"
  OR "Conservation of Antarctic Living Marine Resources"
)
```

A website with Norwegian and English names for international environmental agreements from the Norwegian Environment Agency was used to help translate agreement names (https://www.miljodirektoratet.no/regelverk/konvensjoner/; accessed 24/01/23)


```python
#Termlists
termlist14_ca = ["law of the sea",
                 "diversity beyond national jurisdiction",
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

                 "havrettskonvensjon","Havrettstraktaten",
                 "felles fiskeripolitik",
                 "avtalen om fiske på det åpne hav",
                 "avtalen om havnestatstiltak",
                 "avtalen om fiske på vandrende bestander",
                 "regulering av fisket etter dyphavsarter",
                 "Den nordatlantiske laksevernorganisasjonen",
                 "havstrategidirektiv", 
                 "Konvensjonen for bevaring av det marine miljø", "Oslo-Paris-konvensjonen", 
                 "Isbjørnavtalen"
                ]
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
                 "Stockholmkonvensjonen", "Stockholm-konvensjon"
                ]
                #Terms that need to be used with marine terms

phrasedefault14_ca = r'(?:{})'.format('|'.join(termlist14_ca))
phrasedefault14_ca_case = r'(?:{})'.format('|'.join(termlist14_ca_case))
phrasedefault14_cb = r'(?:{})'.format('|'.join(termlist14_cb))
```


```python
#Search in marine set for generic environmental legislation, and in the whole data for marine specific legislation
Data.loc[(
    (    
        (Data['result_title'].str.contains(phrasedefault14_ca, na=False, case=False)) 
        |(Data['result_title'].str.contains(phrasedefault14_ca_case, na=False, case=True)) 
    )
    |
    (
        (Data['result_title'].str.contains(phrasedefault14_cb, na=False, case=False)) 
        & (Data['marine_terms']==True)
    )
),"tempsdg14_c"] = "SDG14_c"

print("Number of results = ", len(Data[(Data.tempsdg14_c == "SDG14_c")])) 
```


```python
test=Data.loc[(Data.tempsdg14_c == "SDG14_c"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

#### Phrase 2

```
TS =
(
  ("international"
  NEAR/3 ("governance" OR "law$" OR "policy" OR "policies" OR "regulat*" OR "legal*" OR "legislat*" OR "agreement$" OR "treaty" OR "treaties" OR "framework$" OR "instrument$")
  )
  NEAR/15
    ("conservation" OR "sustainab*" OR "ecosystem restoration"
    OR "marine spatial planning" OR "MSP"
    OR "ecosystem based management" OR "area based management" OR "resilience based management"
    OR "coastal zone management" OR "integrated coastal zone planning" OR "ICZM"
    OR "coastal resources management"
    OR "community based management" OR "locally managed marine area$" OR "LMMA$"
    OR "marine spatial planning" OR "spatial management"
    OR "herbivore management area$"
    OR "ecosystem approach*"
    OR "MPA" OR "MPAs" OR "LSMPA$" OR "marine protected area$"
    OR "marine reserve$" OR "ocean reserve$" OR "marine park$"
    OR "marine conservation zone$"
    OR "particularly sensitive sea areas$"
    OR "blue growth" OR "blue econom*"
    )
)
```


```python
#Termlists
termlist14_cc = ["international", 
                 "internasjonal"]

termlist14_cccaps = ["UN", 
                 "FN"]

termlist14_cd = ["governance","policy","policies","regulat","legal","legislat","agreement","treaty","treaties","framework","instrument",
                 "styring","ledelse", "leiing", "politikk", "retningslin", "rammeverk", "styring", "planlegging", "regulativ", "lovgivning", "rett", "juridisk", "lovverk", "forskrift"]

termlist14_ce = ["law", "laws"
                 "lov"] #terms to limit truncation

termlist14_cf = ["conservation","sustainab","ecosystem restoration",
                 "ecosystem based management","area based management","resilience based management",
                 "coastal zone management","integrated coastal zone planning","coastal resources management",
                 "community based management","locally managed marine area$",
                 "marine spatial planning","spatial management",
                 "herbivore management area","ecosystem approach",
                 "protected area", "marine reserve","ocean reserve","marine park",
                 "conservation zone","particularly sensitive sea area",
                 "blue growth","blue econom",

                 "forvalt", "vernet", "miljøvern", "bevart", "bevaring", "fredet", "fredning", "gjenoppbygg", "restaurer", "bærekraft",
                 "økosystembasert forvaltning", "økosystembasert styring", "forvaltningsplaner",
                 "samfunnsforvalt", "bærekraftig forvalt", "berekraftig forvalt", "arealforvaltning",
                 "integrert kystsone", "kystplanlegging", "kystsoneforvaltning",
                 "marint vernområde","marine vernområde","marine verneområde","marine reservat",
                 "naturreservat", "biotopvernområde", "nasjonalpark", "bevarte område",
                 "blåvekst", "blå vekst", "blå økonomi"
                 ]

termlist14_cfcaps = ["MSP", "ICZM", "LMMA", "MPA","LSMPA"] #terms to search case sensitive

phrasedefault14_cc = r'(?:{})'.format('|'.join(termlist14_cc))
phrasespecific14_cccaps = r'\b(?:{})\b'.format('|'.join(termlist14_cccaps))
phrasedefault14_cd = r'(?:{})'.format('|'.join(termlist14_cd))
phrasedefault14_ce = r'(?:{})'.format('|'.join(termlist14_ce))
phrasedefault14_cf = r'(?:{})'.format('|'.join(termlist14_cf))
phrasedefault14_cfcaps = r'(?:{})'.format('|'.join(termlist14_cfcaps))

```


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault14_cc, na=False, case=False))  | (Data['result_title'].str.contains(phrasespecific14_cccaps, na=False, case=False)) )
    & ((Data['result_title'].str.contains(phrasedefault14_cd, na=False, case=False))  | (Data['result_title'].str.contains(phrasedefault14_ce, na=False, case=False)) )
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

```
TS=
("SDG 14" OR "SDGs 14" OR "SDG14" OR "sustainable development goal$ 14"
OR ("sustainable development goal$" AND "goal 14")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 14")
    AND ("life below water")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 13")
    NEAR/50 ("ocean$" OR "marine" OR "sea" OR "seas" OR "fisheries")
    )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
```

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
      |
      (
        (Data['result_title'].str.contains(phrasedefault_sdg_b, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault_sdg_c, na=False, case=False))
      )
      |
      (
         (Data['result_title'].str.contains(phrasedefault_sdg_d, na=False, case=False))
         & (Data['result_title'].str.contains(phrasespecific_sdg_e, na=False, case=False))
      )
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

```
TS=
( "terrestrial" OR "soil" OR "soils"  
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


```python
## The terrestial list
#---------------------------------

termlist15_terr1 = ["terrestrial",
                   "forest", "woodland", "taiga", "jungle", "mangrove", 
                    "peatland", "peat land", "swamp", "wetland", "marsh", "paludal",
                    "farmland", "agricultural land", "cropland", "pasture", "rangeland",
                    "shrub", "meadow", "bushland", "heath",
                    "savanna","grassland","prairie",
                    "dryland", "dry land", "desert", 
                    "mountain", "highland", "alpine", "tundra"
                    "freshwater", "limnic", "inland fish",
                    "brook", "creek",

                    "terrestrisk", "landlevende","villmarksområd",
                    "skog", "jungel",
                    "torv", "torvmos", "torvmyr", "slåttemyr", "myrer", "myrar", "sumper", "sumpar", "våtmark", "våteng", "torvmark",
                    "dyrket mark", "dyrket jord", "dyrka jord", "dyrka mark", "landbruksmark", "utmark", "innmark", "beite",
                    "kratt", "busker", "lynghei",
                    "engmark", "natureng", "kultureng", "engvegeta", "moseeng", "gresseng", "strandeng", "slåttemark", 
                    "prærie", "tørre område",
                    "tørrmark", "ørken", "halvtørre områd",
                    "fjell", "bergtopp", "alpin", 
                    "ferskvann", "ferskvatn", "innlandsfisk", "innsjø"  
                     ]

termlist15_terr2 = ["soil", "soils", "bog", "bogs", "mire", "mires", "fen", "fens", "bush", "bushes", "plains", "steppe",
                    "lake", "lakes", "pond", "ponds", "river", "rivers", "stream", "streams",

                    "jord", "åker", "myr","sump", "eng", "enger", "busk", "elv", "elver", "bekk",
                   ]
                   #Terms where we need to avoid truncation

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
                  "språk", "barnevernet"
                  ]
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
test.iloc[0:5, [0,4,5,6,8]]
```

### SDG 15.1

*15.1 By 2020, ensure the conservation, restoration and sustainable use of terrestrial and inland freshwater ecosystems and their services, in particular forests, wetlands, mountains and drylands, in line with obligations under international agreements*

*Innen 2020 bevare og gjenopprette bærekraftig bruk av ferskvannsbaserte økosystemer og tjenester som benytter seg av disse økosystemene, på land og i innlandsområder, særlig skoger, våtmarker, fjell og tørre områder, i samsvar med forpliktelser i internasjonale avtaler.*


#### Phrase 1
```
TS=
(
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


```python
#Termlists
termlist15_1a = ["protected area","conservation area","conservation zone","Wilderness area","Nature reserve","National park",
                 "Habitat management area","Species management area","Protected landscape",
                 "conserved ecosystem","conservation ecosystem", "protected ecosystem","protecting ecosystem", "protect ecosystem",

                 "vernområde","bevarte område", "bevaringsområde", "naturreservat","biotopvernområde","biosfæreområde","nasjonalpark",
                 "landskapsvern","økosystemforvalt","økosystembasert forvalt",
                 "vernet økosystem","fredningsområde","forvaltningsområde"
                 ]
termlist15_1b = ["protect","preserv","conserv","reforest","re-forest", "rehabilit",
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer","skogplanting", "gjengro",
                 ]
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
```
TS=
(
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


```python
#Termlists
termlist15_1d = ["protect","preserv","conserv","reforest","re-forest", "rehabilit",
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer","skogplanting", "gjengro"
                 ]
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
        & ((Data['result_title'].str.contains(phrasedefault15_1e, na=False, case=False))| (Data['result_title'].str.contains(phrasespecific15_1etrunc, na=False, case=False)))
        & (Data['terrestrial_double_NOT']==True)
    )
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
#Search 2 - in terr

Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_1d, na=False, case=False))
    &(Data['terr_terms']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
test=Data.loc[(Data.tempsdg15_01 == "SDG15_01"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

#### Phrase 3
```
TS=
(
  ("manage" OR "conserve" OR "protect" OR "restore" OR "management" OR "conservation" OR "protection" OR "restoration" OR "sustainable")
  NEAR/15
    ("habitat$"
    OR
      ("ecosystem$" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$" OR "terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
      ) 
    OR 
      ("communit*" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "pollinator$")
      )
    OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
    OR 
      ("diversity" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$")
      )
    OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
    )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```


```python
#Termlists
termlist15_1f = ["protect","preserv","conserv","restore", "restoring", "restoration", "sustainable",
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer", "bærekraft", "berekraft"
                 ]
                 #"vernet"(NO) will also find "vernetiltak"
termlist15_1g = ["habitat",
                 "biodivers","biological diversity","species diversity","functional diversity","genetic diversity","taxonomic diversity",
                 "key species","keystone species","foundation species","habitat forming species","key resource",
                 
                 "leveområd", 
                 "biologisk mangf", "biomangf", "biologiske mangf", "artsmangf", "artsdiversitet", "genetisk mangf", "genetisk diversitet",
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
    #Here an extra line is added compared to Web of Science - where phrase15_1h (diversity etc.) is searched for only within titles that
    #also contain a terrestrial term, allowing subjects such as "forest diversity" to be found. 19 extra results, ca. 17 relevant

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```


```python
test=Data.loc[(Data.tempsdg15_01 == "SDG15_01"), ("result_id", "result_title")]
test.iloc[10:15, ]
```

#### Phrase 4
```
TS=
(  
    ("long term management plan"
    OR "agro-ecological knowledge" OR "agro ecological knowledge"
    OR "bidiversity" OR "biological diversity"
    OR "key biodiversity area$" 
    OR ("KBA$" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR 		"tree$" OR "grassland$" OR "pollinator$"))
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

Note, here we have made a change compared to the string in Web of Science. There, in the topic approach, biodiversity is included alone. Here I have included it with action terms. It is also misspelled in the WoS string which has caused issues in testing. See issue #30 in GitHub.


```python
#Termlists
termlist15_1j = ["long term management plan", "long-term management plan", 
                 "agro-ecological knowledge","agro ecological knowledge",
                 "key biodiversity area", "important sites for biodiversity",
                 "ecotourism","eco-tourism",
                 
                 "langsiktig miljøforvaltning",
                 "nøkkelhabitat","nøkkelbiotop",
                 "økoturis", "øko-turis"
                 ]
termlist15_1k = ["KBA"]      

termlist15_1l = ["promot" , "enable" , "increase" , "establish" , "implement" , "assure" , "ensur",
                 "muliggjør", "mogeleggjer", "mogleggjer", "øker", " øke ", " auke ", "etabler", "sørge for", "sørger for"]           
termlist15_1m = ["biodiversit","biological diversity",
                 "biologisk diversitet", "biologisk mangf", "biologiske mangf", "biomangf", "artsmangf"] 
                 #Note that "biodiversit" will cover "biodiversitet" (NO) and e.g. soil biodiversity

termlist15_1n = ["sustainabl", "responsibl",
                 "bærekraft", "berekraft", "ansvarlig", "ansvarleg"]
termlist15_1o = ["ecosystem service","soil","freshwater",
                 "økosystemtjenest", "ferskvann", "ferskvatn", "jord "]
                 #a space is included after "jord"(NO) to prevent "jordbruk"

termlist15_1p = ["sustainabl", "responsibl", "environmental", "ecological", "ecosystem approach",
                 "bærekraft", "berekraft", "ansvarlig", "miljø", "økologisk", "økosystemtilnærm", "økosystembasert forvaltning"]
termlist15_1q = ["natural resource", "groundwater", "freshwater fish", "salmon", "trout", "hunting", "trapping", "forestry", "recreation", "tourism", "grazing", "firewood", "fire wood", "fuel wood",
                 "naturressurs", "grunnvann", "grunnvatn", "ferskvannsfisk", "innlandsfisk", "ferskvannskreps", "laks", "ørret", "auret", "jakt", "fangst", "skogbruk", "fritid", "tursti", "turist", "turism", "beite", "fyringsved", "bjørkeved"]
                 #"ved" (NO: firewood) is difficult in Norwegian because it is often combined with other words (can't stop truncation), AND is a preposition (ved also = "by")
                 #Here we have dropped the last NEAR combo as an unneccesary restriction
                 #Fishing terms in Norwegian are limited to freshwater since there is so much marine research. 
                  #44 results dropped, nearly all marine, should be found by SDG14
                  #Salmon and trout included as partially freshwater
termlist15_1r = ["manag", "sustainable us", "responsible us", "usage", "govern", "administr", "planning",
                 "forvalt", "bruk", "bruker", "planlegg", "styring", "ledelse", "leiing"]
                 #Generic terms to combine with 15_1p, and the terrestrial terms

phrasedefault15_1j = r'(?:{})'.format('|'.join(termlist15_1j))
phrasespecific15_1k = r'\b(?:{})\b'.format('|'.join(termlist15_1k))
phrasedefault15_1l = r'(?:{})'.format('|'.join(termlist15_1l))
phrasedefault15_1m = r'(?:{})'.format('|'.join(termlist15_1m))
phrasedefault15_1n = r'(?:{})'.format('|'.join(termlist15_1n))
phrasedefault15_1o = r'(?:{})'.format('|'.join(termlist15_1o))
phrasedefault15_1p = r'(?:{})'.format('|'.join(termlist15_1p))
phrasedefault15_1q = r'(?:{})'.format('|'.join(termlist15_1q))
phrasedefault15_1r = r'(?:{})'.format('|'.join(termlist15_1r))
```


```python
#Search 1 - in double NOT

Data.loc[(
    (
        (
            (Data['result_title'].str.contains(phrasedefault15_1j, na=False, case=False))
            | (Data['result_title'].str.contains(phrasespecific15_1k, na=False, case=False))
        )   
        |
        (
            (Data['result_title'].str.contains(phrasedefault15_1l, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault15_1m, na=False, case=False))     
        )
        |
        (
            (Data['result_title'].str.contains(phrasedefault15_1n, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault15_1o, na=False, case=False))     
        )
        |
        (
            (Data['result_title'].str.contains(phrasedefault15_1p, na=False, case=False))
            & (Data['result_title'].str.contains(phrasedefault15_1q, na=False, case=False))
        )
    )
    &(Data['terrestrial_double_NOT']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 


#Search 2 - in terrestrial terms

Data.loc[(  
        (Data['result_title'].str.contains(phrasedefault15_1p, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault15_1r, na=False, case=False)) #only searching in the terrestrial terms set, as these are generic terms
        & (Data['terr_terms']==True)
),"tempsdg15_01"] = "SDG15_01"

print("Number of results = ", len(Data[(Data.tempsdg15_01 == "SDG15_01")])) 
```

#### Phrase 5
```
TS=
(
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


```python
#Termlists
termlist15_1s = ["Convention on Biological Diversity",
                 "Convention to Combat Desertification",
                 "Convention on International Trade in Endangered Species of Wild Fauna and Flora",
                 "Nagoya","Plant Genetic Resources for Food and Agriculture","International Seed Treaty","Plant Treaty",
                 "Convention on Wetlands of International Importance",
                 "Bonn convention", "Convention on the Conservation of Migratory Species of Wild Animals",

                 "Konvensjon om biologisk mangfold", "Konvensjonen om biologisk mangfold", "biodiversitetskonvensjon",
                 "Naturmangfoldloven", "lov om vern av naturens mangfold",
                 "Konvensjonen om internasjonal handel med truede dyr", "handel med truede og sårbare arter",
                 "Den internasjonale plantetraktaten",
                 "Ramsarkonvensjon", "Ramsar-konvensjon", "Våtmarkskonvensjonen",
                 "Bonnkonvensjon", "Bonn-konvensjon", "konvensjonen om bevaring av trekkende ville dyr"
                 ]
termlist15_1t = ["UNCCD", "CITES", "ITPGRFA"]      

termlist15_1u = ["Framework Convention on Climate Change", "UNFCCC", "CBD",
                 "world heritage convention",
                 "European landscape convention",

                 "Klimakonvensjon.*", "rammekonvensjon om klimaendring.*",
                 "verdensarvkonvensjon.*",
                 "landskapskonvensjon.*"
                 ]       

termlist15_1v = ["ecosystem", "habitat", "environment", "biotop", "ecolog", "species", "plant", "animal", "organism", "flora", "fauna", "biodivers", "biological diversit",
                 "økosystem", "leveområd", "miljø", "økolog", "rovdyr", "pattedyr", "dyreart", "dyrart", "planter", "artsmangf", "biologisk diversit", "biologisk mangf", "biomangf"] 
termlist15_1w = ["art", "arter"]

phrasedefault15_1s = r'(?:{})'.format('|'.join(termlist15_1s))
phrasespecific15_1t = r'\b(?:{})\b'.format('|'.join(termlist15_1t))
phrasespecific15_1u = r'\b(?:{})\b'.format('|'.join(termlist15_1u))
phrasedefault15_1v = r'(?:{})'.format('|'.join(termlist15_1v))
phrasespecific15_1w = r'\b(?:{})\b'.format('|'.join(termlist15_1w))
```


```python
#Search 1

Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_1s, na=False, case=False))
        | (Data['result_title'].str.contains(phrasespecific15_1t, na=False, case=True)) 
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

```
TS=
(
  (
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


```python
#Termlists
termlist15_2a = ["sustainable forest","sustainable woodland","sustainable silvicultur","sustainable arboricultur",
                 "protected forest", "reserved forest", 
                 "UN strategic plan for forests", "global forest goals",

                 "bærekraftfig skog", "bærekraftig silvikultur", "berekraftig skog", "berekraftig silvikult",
                 "vernet skog", "vern av skog", "bevarte skog", "bevart skog", "freda skog", "skogvern", "verneområder i skog",
                 "strategiske plan for skog"
                 ]
termlist15_2acaps = ["UNSPF", "GFG"]

termlist15_2b = ["sustainab", "responsibl", "environmental", "ecological",
                 "bærekraftig", "berekraftig", "ansvarlig", "ansvarleg","miljøbevisst", "miljøvennlig","miljøvennleg", "økologisk"]

termlist15_2c = ["manag", "govern", "development", "administ", "planning", "policy", "policies",
                 "practice", "method", "forestry",
                 "cutting", "logging", "felling", "clearing", "lopping", "limbing", "thinning", "creaming", "pruning", "rotation",
                 "planting tree", "tree planting", "drainage", 
                 "forest area change",
                 "above ground biomass",
                 "protected area", "term management plan",
                 "forest under certification",
                 "certified forest area",

                 "forvalt", "styring", "ledelse", "leiing", "utvikling", "planlegg", "politikk", "retningslin",
                 "praksis", "metode", "skogskjøtsel", "skogpleie", "skogsvirke",
                 "tynning", "gjødsling", "hogst", "hogge", "stelle",
                 "planting", "foryngelse", "gjengro", "attgro", "restaurer", "drenering",
                 "skogområde", "skogvolum", "skogdek", "skogbevokste områd", "skogbevokst områd","skogareal",
                 "miljøvern", "bevaret", "bevaring", "fredet", "fredning", "frivillig vern",
                 "miljøsertifi"
                 ]
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

```
TS=
(
  "deforest*"
  OR ("*forest*" NEAR/3 ("loss" OR "degrad*"))
  OR ("lost" NEAR/3 "forest area")
  OR
    (
      ("*forest*" OR "woodland$" OR "silvicultur*" OR "arboricultur*")
      NEAR/5 ("decreas*" OR "reduc*" OR "degrad*" OR "mitigat*" OR "disappear*" OR "lost" OR "loss")
    )
  OR ("REDD" NEAR/15 ("UN" OR "United Nations"))
)
```


```python
#Termlists
termlist15_2e = ["deforest", "de-forest",
                 "avskog", "skogforringelse", "skogtap"]
                 #skogforringelse (NO: forest degredation), and is included here instead of below because in Norwegian this is one word specific to forests.

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

termlist15_2h = ["REDD"] #Can use a case-sensitive search here instead of combining with UN

phrasedefault15_2e = r'(?:{})'.format('|'.join(termlist15_2e))
phrasedefault15_2f = r'(?:{})'.format('|'.join(termlist15_2f))
phrasespecific15_2ftrunc = r'(?:{})\b'.format('|'.join(termlist15_2f_trunc))
phrasedefault15_2g = r'(?:{})'.format('|'.join(termlist15_2g))
phrasespecific15_2gtrunc = r'\b(?:{})\b'.format('|'.join(termlist15_2gtrunc))
phrasedefault15_2h = r'(?:{})'.format('|'.join(termlist15_2h))
```


```python
#Search 1
Data.loc[(
    (Data['result_title'].str.contains(phrasedefault15_2e, na=False, case=False)) 
    | (Data['result_title'].str.contains(phrasedefault15_2h, na=False, case=True)) 
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

```
TS=
(
  (
    (
      ("increas*" OR "expand*" OR "restor*" OR "rehabilitate")
      NEAR/5 ("cover*" OR "area$" OR "zone$" OR "*land$" OR "silvicultur*")
    )
  OR "restore" OR "restoration" OR "rehabilitat*"
  OR "restor*" OR "rehabilita*"
  )
  NEAR/5 ("*forest*" OR "woodland$")
)
OR TS=("afforestr*" OR "reforestr*")
```


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
```
TS=
(
  (
        ("desertif*"
        OR (("increas*" OR "expand*") NEAR/5 ("desert$" OR "dryland$"))
        )
  )
  OR "United Nations Convention to Combat Desertification"
  OR "UN Convention to Combat Desertification"
  OR "UNCCD"
)
```


```python
#Termlists
termlist15_3a = ["desertific", "convention to combat desertification",
                "ørkenspredning", "ørkenspreiing", "forørkning", "konvensjon for bekjempelse av ørkenspredning", "forørkningskonvensjon"
                ]
termlist15_3acaps = ["UNCCD"]

termlist15_3b = ["increas", "expand",
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
    |(Data['result_title'].str.contains(phrasedefault15_3acaps, na=False, case=True)) 
    | (
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

```
TS=
(
  ("desert$" OR "desertif*" OR "drought" OR "flood$" OR "dryland$")
  NEAR/15
      ("soil structure" OR "soil fertility" OR "soil health"
      OR ("quality" NEAR/5 ("soil$" OR "land"))
      OR ("degrad*" NEAR/3 ("land$" OR "soil$"))
      OR (("erosion" OR "eroded") NEAR/5 ("land$" OR "soil$"))
      )
)
```


```python
#Termlists
termlist15_3d = ["desertific", "drought", "flood", "drylands", "dryland area", 
                 "ørkenspredning", "ørkenspreiing", "halvtørre område", "tørrland"]

termlist15_3e = ["soil structure" , "soil fertility" , "soil health",
                 "soil quality", "land quality",
                 "jordskjelett", "jordstruktur", "fruktbar jord", "jordhelse",
                 "jordkvalitet", "kvalitetsjord"]

termlist15_3f = ["land", "soil",
                 "jord", "dyrket mark", "dyrkamark", "kultivert mark"]

termlist15_3g = ["quality", "degrad", "erosion", "eroded",
                 "kvalitet", "forring", "erosjon", "jordtap"]

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

```
TS=
(
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
  NEAR/15
      ("desert$" OR "desertif*" OR "dryland$" OR "dry land$"
      OR (("arid" OR "semi arid" OR "semi-arid" OR "sub humid" OR "sub-humid") NEAR/3 ("area*" OR "land*"))
      OR "grassland$" OR "savanna$" OR "prairie$" OR "rangeland$"
      OR "soil$"
      )
)
```


```python
#Termlists

termlist15_3h = ["aridificat", "soil pollution", "soil loss"] #Translations of these (e.g."uttørking"(NO)) are combined with soil terms in 3j

termlist15_3i = ["soil",
                 "dyrket mark", "dyrkamark", "dyrka mark", "dyrkamark",  "kultivert mark"]
termlist15_3itrunc = ["land", "jord", "jordbruk"] 
#"land" is not truncated because in Norwegian it is a part of many place names, also in english (e.g. LANDSAT, Iceland...), and "jord"(NO) due to "fjord"
termlist15_3j = ["quality", "degrad", "erosion", "eroded", "salinisat", "alkalinisat", "acidificat", "contaminat", "pollution", "biodiversity loss",
                 "kvalitet", "forring", "uttørking", "erosjon", "jordtap", "salinering", "forsalting", "forsuring", "forurein", "forurensing"]

termlist15_3k = ["declin","decreas","reduc","degrad","lower","loss",
                 "nedgang", "mindre", "forring", "lavere", "lægre", "lågare"]
termlist15_3k_trunc = ["tap", "tapt", "tapte"]
termlist15_3l = ["biodiversity","soil","vegetation","groundwater",
                 "biodiversitet", "biologisk diversitet", "biologisk mangf", "biomangf", "jord", "vegetasjon", "grunnvann", "grunnvatn"]

termlist15_3m = ["desert", "drylands", "dryland area","sub-humid", "sub humid", "semi-arid", "semiarid", "grassland", "savanna", "prarie", "rangeland",
                 "ørken", "halvtørr", "tørrland"]
termlist15_3mtrunc = ["arid"]

phrasedefault15_3h = r'(?:{})'.format('|'.join(termlist15_3h))
phrasedefault15_3i = r'(?:{})'.format('|'.join(termlist15_3i))
phrasespecific15_2itrunc = r'\b(?:{})\b'.format('|'.join(termlist15_3itrunc))
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
        ((Data['result_title'].str.contains(phrasedefault15_3i, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific15_2itrunc, na=False, case=False)))
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

```
TS=
(
  ("desert$" OR "desertif*" OR "dryland$" OR "dry land$"
  OR (("arid" OR "semi arid" OR "semi-arid" OR "sub humid" OR "sub-humid") NEAR/3 ("area*" OR "land*"))
  OR "grassland$" OR "savanna$" OR "prairie$" OR "rangeland$"
  )
  NEAR/15 (("soil" OR "land") NEAR/3 ("productivity" OR "fertility"))
)
OR
TS=
  (
    ("land degradation neutrality" OR "LDN")
    AND "land degradation"
  )
```

Note, "land degredation" is already covered by phrase 3, and "LDN" only brings noise here, so it is not included (low-dose naltrexone).


```python
#Termlists

termlist15_3n = ["desert", "drylands", "dryland area","sub-humid", "sub humid", "semi-arid", "semiarid", "grassland", "savanna", "prarie", "rangeland",
                 "ørken", "halvtørr", "tørrland"]
termlist15_3ntrunc = ["arid"]

termlist15_3o = ["soil",
                 "jord", "dyrket mark", "dyrkamark", "dyrka mark","kultivert mark"]
termlist15_3otrunc = ["land"] 
#"land" is not truncated because in Norwegian it is a part of many place names, also in english (e.g. LANDSAT, Iceland...)
termlist15_3p = ["fertility", "productivity",
                 "fruktbar", "fertilitet", "produktivitet"]
                
phrasedefault15_3n = r'(?:{})'.format('|'.join(termlist15_3n))
phrasespecific15_2ntrunc = r'\b(?:{})\b'.format('|'.join(termlist15_3ntrunc))
phrasedefault15_3o = r'(?:{})'.format('|'.join(termlist15_3o))
phrasespecific15_2otrunc = r'\b(?:{})\b'.format('|'.join(termlist15_3otrunc))
phrasedefault15_3p = r'(?:{})'.format('|'.join(termlist15_3p))
```


```python
#Search 1
phrase15_3nq = Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault15_3n, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_2ntrunc, na=False, case=False)))
    & (
        ((Data['result_title'].str.contains(phrasedefault15_3o, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific15_2otrunc, na=False, case=False)))
        & (Data['result_title'].str.contains(phrasedefault15_3p, na=False, case=False))
      )
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

Since phrase 1 and 2 use many of the same terms, they are both handled here. For the original phrase 2, I have simplified by only taking the terms "sustainable", "ecologial" and "environmental" and dropped the combination with use, management etc. as this is a title search. In an abstract search they should be included.

```
#Phrase 1
TS=
(
  (
    (
      ("manage" OR "managing" OR "managed" OR "conserve" OR "conserving" OR "protect" OR "protecting" OR "protected" OR "restore" OR "restoring"
      OR "management" OR "conservation" OR "protection" OR "restoration"
      OR "Protected area$" OR "Wilderness area$" OR "Nature reserve$" OR "National park$" OR "Natural monument$" OR "Natural feature$" OR "Protected landscape$"
      OR "CITES"
      ) 
      AND 
        ("ecosystem$" OR "habitat$"
        OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
        OR (("diversity" OR "communit*") NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
        OR (("covered" OR "cover*") NEAR/5 ("green" OR "vegetat*" OR "*forest$" OR "shrub$" OR "tree$" OR "pasture$" OR "cropland$" OR "grassland$" OR "wetland$")) 
        )
    )
  OR 
    (
      ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "higher" OR "upgrad*" OR "advance" OR "develop" OR "ensure" OR "maintain*" OR "preserv*" OR "sustain" OR "decreas*" OR "reduc*" OR "restrict*" OR "degrad*" OR "lowering" OR "lower$" OR "lowered" OR "declin*" OR "deterior*" OR "degrad*" OR "coping" OR "cope" OR "adapt*" OR "resilien*" OR "assess*" OR "examin*" OR "evaluat*" OR "measur*" OR "monitor*"
      ) 
      NEAR/5 
        ("ecosystem$" OR "habitat$"
        OR "biodiversity" OR "biological diversity" OR "species diversity" OR "functional diversity" OR "genetic diversity" OR "taxonomic diversity"
        OR (("diversity" OR "communit*") NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR "key species" OR "keystone species" OR "foundation species" OR "habitat forming species" OR "key resource$"
        OR (("covered" OR "cover*") NEAR/5 ("green" OR "vegetat*" OR "*forest$" OR "shrub$" OR "tree$" OR "pasture$" OR "cropland$" OR "grassland$" OR "wetland$")) 
        ) 
    ) 
  OR "Habitat management area$" OR "Species management area$"
  OR "key biodiversity area$" OR "KBA" OR "KBAs"
  OR "important sites for biodiversity"
  OR "Mountain Partnership"
  OR "Mountain Green Cover Index"
  OR "Convention on Biological Diversity" OR "CBD"
  OR "Convention on International Trade in Endangered Species of Wild Fauna and Flora" 
  )
  AND ("mountain*" OR "alpine" OR "highland$" OR ("fell$" NEAR/5 "Lapland"))
)

#Phrase 2
TS=
(
  (
    (
      ("sustainabl*" OR "environmental*" OR "ecological*")
      NEAR/3 ("manag*" OR "use" OR "using" OR "govern*" OR "development" OR "administrat*" OR "planning")
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


```python
#Termlists
termlist15_4a = ["mountain", "alpine", "highland",                
                 "fjell", "alpin", "vidde", "vidda"
                ]

termlist15_4b = ["manag", "conserv", "protect", "restor",
                 "Protected area","Wilderness area","Nature reserve","National park","Natural monument","Natural feature","Protected landscape",
                 "increas","strengthen","improv","enhanc","better","higher","upgrad","advance","develop","ensure","maintain","preserv","sustain",
                 "decreas","reduc","restrict","degrad","lower","declin","deterior",
                 "coping","cope","adapt","resilien",
                 "assess","examin","evaluat","measur","monitor",
                 "sustainable", "ecological", "environmental",

                 "styring", "forvalt", "vernet", "verna", "verne", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaur",
                 "vernområde", "verneområde", "naturreservat", "biotopvernområde", "nasjonalpark", "bevarte område", "bevaringsområde",
                 "øker", "styrk", "forbedr", "bedring", "betring", "oppgrad", "viderefør", "sikre", "vedlikehold", "vedlikehald", "oppretthold", "opprethald",
                 "reduser", "nedgang", "avgrens", "forring", "nedsatt", "nedsett", 
                 "tåle", "tilpass", "resilien",
                 "overvåk", "vurder", "evaluer", "måle", "monitor",
                 "bærekraft", "berekraft", "økologi", "miljø"
                ]

termlist15_4c = ["ecosystem","habitat",
                 "biodiversity","diversity",
                 "key species","keystone species","foundation species","habitat forming species","habitat-forming species","key resource",
                 "cover",

                 "økosystem", "miljø", "leveområd",
                 "mangfold", "mangfald", "diversitet", 
                 "nøkkelart", "flaggskipsart", "paraplyart", "nøkkelressurs",
                 "dekning", "dekke"
                 ]

termlist15_4d = ["Habitat management area", "Species management area",
                 "key biodiversity area", "important sites for biodiversity",
                 "Mountain Partnership", "Mountain Green Cover Index",
                 "Convention on Biological Diversity", 
                 "Convention on International Trade in Endangered Species of Wild Fauna and Flora",
                 
                 "områdevern", "økosystembasert forvalt", "økosystembasert styring", "forvaltningsplan", "bærekraftig forvalt", "berekraftig forvalt","arealforvaltning", 
                 "artsforvaltning", "naturmangfoldloven", "lov om vern av naturens mangfold",
                 "Konvensjonen om biologisk mangfold", "Konvensjon om biologisk mangfold", "biodiversitetskonvensjon", 
                 "Konvensjonen om internasjonal handel med truede dyr", "naturmangfoldloven"
                ]

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
        | (Data['result_title'].str.contains(phrasespecific15_4d_case, na=False, case=True))
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
```
TS=
(
  ("degrad*" OR "declin*" OR "loss" OR "lost" OR "destruct*" OR "disappear*" OR "fragmentat*")
  NEAR/5
      ("ecosystem$" OR "habitat$" OR "biotope$"
      OR ("communit*" NEAR/5 ("ecolog*" OR "species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      )
)
AND
TS=("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
```


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
```
TS=
(
    ("degrad*" OR "declin*" OR "loss" OR "lost" OR "destruct*" OR "disappear*")
    NEAR/5
      ("biodiversity" OR "biological diversity"
      OR (("diversity" OR "species") NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      )
)
AND
TS=("terrestrial" OR "soil" OR "soils" OR "*forest*" OR "woodland$" OR "taiga" OR "jungle" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$")
```


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
```
TS=
(
  (
    ("manage" OR "managing" OR "managed" OR "conserve" OR "conserving" OR "protect" OR "protecting" OR "restore" OR "restoring"
    OR "management" OR "conservation" OR "protection" OR "restoration" OR "rehabilit*" OR "preserve" OR "preservation" OR "preserved"
    ) 
    AND 
        ("biodiversity" OR "biological diversity" 
        OR "key biodiversity area$" 
        OR ("KBA$" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR "important sites for biodiversity" 
        OR ("diversity" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
        OR (("threatened" OR "near extinct*" OR "at risk" OR "endanger*" OR "vulnerable" OR "protected" OR "red list*") NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$"))
        OR "Red List Index"
        OR "RLI" OR "Red List" OR "IUCN" OR "International Union for Conservation of Nature"
        )
  )
OR
  (
    ("increas*" OR "strengthen*" OR "improv*" OR "enhanc*" OR "better" OR "higher" OR "upgrad*" OR "advance" OR "develop" OR "ensure" OR "maintain*" OR "preserv*" OR "sustain" OR "decreas*" OR "reduc*" OR "restrict*" OR "degrad*" OR "lowering" OR "lower$" OR "lowered" OR "declin*" OR "deterior*" OR "degrad*" OR "coping" OR "cope" OR "adapt*" OR "resilien*" OR "assess*" OR "examin*" OR "evaluat*" OR "measur*" OR "monitor*"
    ) 
    NEAR/5 
      ("biodiversity" OR "biological diversity" 
      OR "key biodiversity area$" 
      OR ("KBA$" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      OR "important sites for biodiversity" 
      OR ("diversity" NEAR/5 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "mosses" OR "tree$" OR "grassland$" OR "pollinator$"))
      OR (("threatened" OR "near extinct*" OR "at risk" OR "endanger*" OR "vulnerable" OR "protected" OR "red list*") NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$"))
      OR "Red List Index"
      OR "RLI" OR "Red List" OR "IUCN" OR "International Union for Conservation of Nature"
      )
  )
)
NOT TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "salivary microbio*" OR "gut microbio*" OR "skin microbio*" OR "oral microbiome" OR "gut flora" OR "skin flora" OR "immunologi*" OR "immunology" OR "hormon*" OR "parasite*" OR "syndrome" OR "vector$" OR "enzyme*" OR "infected" OR "infection" OR "infect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```


```python
#Termlists

termlist15_5f = ["manag", "conserv", "protect", "restor", "rehabilit", "preserv",
                 "increas","strengthen","improv","enhanc","better","higher","upgrad","advance","develop","ensure","maintain","preserv","sustain",
                 "decreas","reduc","restrict","degrad","lower","declin","deterior",
                 "coping","cope","adapt","resilien",
                 "assess","examin","evaluat","measur","monitor",

                 "styring", "forvalt", "verne", "verna", "vern av", "miljøvern", "bevare", "betring", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaur",
                 "øker", "styrk", "forbedr", "bedring", "oppgrad", "viderefør", "sikre", "vedlikehold", "vedlikehald", "oppretthold", "opprethald",
                 "reduser", "nedgang", "avgrens", "forring", "nedsatt", "nedsett", 
                 "tåle", "tilpas", "resilien",
                 "overvåk", "overvak", "vurder", "evaluer", "måle", "monitor"
                 ]


termlist15_5g = ["biodiversity","species diversity",
                "key biodiversity area","important sites for biodiversity",
                "red list", "International Union for Conservation of Nature",

                "artsmangf", "artsdiversitet", "biomangf", "biologisk mangf", "biologiske mangf", 
                "artsforvaltning", "naturmangfoldloven","lov om vern av naturens mangfold",
                "rødlist", "rød list", "raudlist", "raud list",
                "trua art", "trued art", "truede art"
                 ] 
                 #"trua art" (NO) etc are included as phrases here because both terms are easily creating noise with automatic truncation
                 #The english combinations and "truet"(NO) are covered by h+i below
termlist15_5g_case = ["KBA", "KBAs", "CBD", "RLI", "IUCN"]

termlist15_5h = ["threatened","near extinct","at risk","endanger","vulnerable","protected","red list",
                 "diversity",
                 "truet", "truga", "utryddingstru", "utrydjingstruga", "utsatte", "utsette", "sårbar", "vernet", "verna", "fredet", "freda", "rødlist", "rød list", "raudlist", "raud list",
                 "diversitet", "mangfold", "mangfald"
                 ]

termlist15_5i = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl", "moser", "mosar", "trær"
                 ]
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
```
TS=
(
  ("extinction" OR "loss" OR "going extinct")
  NEAR/15
        (
          ("threatened" OR "near extinct*" OR "at risk" OR "endanger*" OR "vulnerable" OR "protected" OR "red list*")
          NEAR/3 ("species" OR "plant*" OR "animal$" OR "organism$" OR "flora" OR "fauna" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$")
        )
)
NOT TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```


```python
#Termlists

termlist15_5j = ["threatened","near extinct","at risk","endanger","vulnerable","protected","red list",
                 "truet", "truga", "trua ", " trued", "truede", "utryddingstru", "utrydjingstruga", "utsatte", "utsette", "sårbar", "vernet", "verna", "fredet", "freda", "rødlist", "rød list", "raudlist", "raud list"
                 ] #the spaces before/after "trua"(NO), "trued"(NO) are intentional (to avoid e.g. "construed")

termlist15_5k = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"
                 ]
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
```
TS=
(
  (
    ("share$" OR "sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$" OR "ownership")
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


```python
#Termlists
termlist15_6a = ["share", "sharing", "equitab", "equal", "fair", "access", "right", "ownership",
                 "deling", "deler", " dele"  "tilgang", "rett", "rettferd", "eierskap", "eigarskap"
                 ] #spaces around "dele"(NO) intentional to avoid truncation

termlist15_6b = ["genetic resource", "gene resource", 
                 "traditional knowledge", "indigenous knowledge", "autochthonous knowledge", "local knowledge",

                 "genetiske ressurs", "genressurs", "plantegenetiske ressurs", "dyrgenetiske ressurs", "dyregenetiske ressurs",
                 "tradisjonelle kunnskap", "tradisjonell kunnskap", "urfolkskunnskap" 
                ]

termlist15_6c = ["ecosystem", "biotop", "diversity", "species", "plant", "animal", "organism",
                 "økosystem", "diversit", "mangfold", "mangfald", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "dyrgenetiske", "dyrgenetiske"
                 ] 
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
```
#Phrase 2
TS=
(
  (
    ("share$" OR "sharing" OR "equitab*" OR "equal" OR "fair" OR "access" OR "accessing" OR "accessib*" OR "right$" OR "ownership")
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
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem" OR "public health" OR "national health" OR "healthcare" OR "health care" OR "epidemiology" OR "health effect$") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))

#Phrase 3
TS=
(
  ("genetic resource$" OR "gene resource$*"
  OR ("knowledge" NEAR/3 ("traditional" OR "indigenous" OR "autochthonous" OR "local"))
  )
  AND
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


```python
#Termlists
#Re-use 6a and 6b

termlist15_6d = ["benefit", "results", "transfer", "technolog", "participat", "product", "monetary", "royalties", "compensat", "bioprospect",
                 "fordel", "gevinst", "resultat", "overfør", "teknologi", "deltak", "finansiel", "kompensasj", "godtgjørelse", "godtgjer", "bioprospekt"] 

termlist15_6e = ["Nagoya", "Convention on biological diversity", "Access and benefit-sharing", "Access and benefit-sharing", "Bonn guideline",
                 "Plant Genetic Resources for Food and Agriculture",
                 "Konvensjonen om biologisk mangfold", "biodiversitetskonvensjon", "Den internasjonale plantetraktaten"
                ] 
termlist15_6e_case = ["CBD","ABS","PGRFA"]

phrasedefault15_6d = r'(?:{})'.format('|'.join(termlist15_6d))
phrasedefault15_6e = r'(?:{})'.format('|'.join(termlist15_6e))
phrasedefault15_6e_case = r'(?:{})'.format('|'.join(termlist15_6e_case))
```


```python
#Search 1
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_6a, na=False, case=False)) 
        & (Data['result_title'].str.contains(phrasedefault15_6b, na=False, case=False))
        & (Data['result_title'].str.contains(phrasedefault15_6d, na=False, case=False))
        & (Data['terrestrial_double_NOT']==True)
    )
    |
    (
        (Data['result_title'].str.contains(phrasedefault15_6e, na=False, case=False)) 
        & ((Data['result_title'].str.contains(phrasedefault15_6b, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_6e_case, na=False, case=True)))
        & (Data['terr_terms']==True)
    )
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
```
TS=
(
  ("poach*" OR "trafficking" OR "trafficked" OR "smuggl*")
  NEAR/15
      (
        ("protect*" OR "endanger*" OR "threat*" OR "extinct*" OR "vulnerable")
        NEAR/5 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$")
       
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```


```python
#Termlists
termlist15_7a = ["poach", "traffick", "smuggl",
                 "krypskyt", "ulovlig", "ulovleg", "smugl", 
                 ]

termlist15_7b = ["protected", "endanger", "threat", "extinct", "at risk", "vulnerable", "red list",
                 "truet", "truga", "utryddingstru", "utrydjingstruga", "utsatte", "utsette", "sårbar", "vernet", "verna", "fredet", "freda", "rødlist", "rød list", "raudlist", "raud list"
                 ]

termlist15_7c = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"
                 ]  
termlist15_7c_trunc = ["art", "arter", "dyr"]                                  

termlist15_7d = ["rosewood" , "kosso" , "elephant" , "rhino" , "ivory" , "pangolin" , "turtle" , "tortoise" , "big cat" , "tiger" , "glass eel",
                 "elefant", "neshorn", "elfenbein", "elfenben", "skilpadde", "store katt", "glassål"
                 "trua art", "trued art", "truede art"
                 ]
                 #The term for "trua art" etc is added as a phrase here since "trua" could be noisy alone

phrasedefault15_7a = r'(?:{})'.format('|'.join(termlist15_7a))
phrasedefault15_7b = r'(?:{})'.format('|'.join(termlist15_7b))
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
            ((Data['result_title'].str.contains(phrasedefault15_7b, na=False, case=False)) 
            & ((Data['result_title'].str.contains(phrasedefault15_7c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_7c_trunc, na=False, case=False)))
            )
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
```
TS=
(
  (
    (
      ("protected" OR "endanger*" OR "threatened*" OR "extinct*" OR "vulnerable")   
      NEAR/5 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "wildlife" OR "insect$" OR "amphibian$" OR "bird$" OR "rosewood" OR "kosso" OR "elephant$" OR "rhino*" OR "ivory" OR "pangolin$" OR "reptile$" OR "turtle$" OR "tortoise$" OR "big cat$" OR "tiger$" OR "glass eel$")
    )
    AND
        (
          ("illegal*" OR "illicit*" OR "criminal" OR "crime")
          NEAR/15
              ("product$" OR "manufact*" OR "merchandise$" OR "artifact*" OR "fabricat*" OR "handicraft$" OR "handiwork$"
              OR "market$*" OR "supply" OR "supplier$" OR "supplied" OR "demand" OR "trade" OR "trading" OR "purchas*" OR "livlihood$"
              )
        )
  )
  AND ("market$*" OR "supply" OR "supplier$" OR "supplied" OR "demand" OR "trade" OR "trading" OR "purchas*" OR "livlihood$")
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```


```python
#Termlists

#Re-use b, c, c_trunc and d
termlist15_7e = ["illegal", "illicit", "criminal", "crime",
                 "ulovlig", "ulovleg", "krim"
                 ]

termlist15_7f = ["product" , "manufact" , "merchandise" , "artifact" , "fabricat" , "handicraft" , "handiwork",
                 "market" , "supply" , "supplier" , "supplied" , "demand" , "trade" , "trading" , "purchas" , "livelihood",
                 "ivory",
                 "produkt", "varer", "produser", "gjenstand", "lager", "håndverk", "handverk",
                 "marked", "marknad", "etterspørsel", "tilbud", "tilbod", "handel", "kjøp", "salg", "levebrød", "inntektskilde", "inntektskjelde",
                 "elfenbein", "elfenben"
                 ]

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
            ((Data['result_title'].str.contains(phrasedefault15_7b, na=False, case=False)) 
            & ((Data['result_title'].str.contains(phrasedefault15_7c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_7c_trunc, na=False, case=False)))
            )
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
```
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


```python
#Termlists

#Re-use b, c, c_trunc and d over
termlist15_7g = ["Convention on International Trade in Endangered Species of Wild Fauna and Flora",
                 "Konvensjonen om internasjonal handel med truede dyr", "handel med truede og sårbare arter", "internasjonal handel med truede arter"]

termlist15_7g_case = ["CITES"]

phrasedefault15_7g = r'(?:{})'.format('|'.join(termlist15_7g))
phrasedefault15_7g_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_7g_case))
```


```python
#Search 1
Data.loc[(
    (
        ((Data['result_title'].str.contains(phrasedefault15_7g, na=False, case=False)) | (Data['result_title'].str.contains(phrasedefault15_7g_trunc, na=False, case=False)))
        & 
        (
            ((Data['result_title'].str.contains(phrasedefault15_7b, na=False, case=False)) 
            & ((Data['result_title'].str.contains(phrasedefault15_7c, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_7c_trunc, na=False, case=False)))
            )
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

### SDG 15.8

*15.8 By 2020, introduce measures to prevent the introduction and significantly reduce the impact of invasive alien species on land and water ecosystems and control or eradicate the priority species*

*Innen 2020 innføre tiltak for å unngå innføring og spredning av fremmede arter for å redusere fremmede arters påvirkning på land- og vannbaserte økosystemer i betydelig grad, og dessuten kontrollere eller utrydde prioriterte fremmede arter*

In some of the phrases I have added an additional term list specific for using these strings for Norwegian research. It contains Latin and Norwegian names for terrestrial and limnic species deemed "very high risk" in the Norwegian black list of introduced species (2018, newest version; https://www.artsdatabanken.no/fremmedartslista2018)

#### Phrase 1
```
TS=
(
  ("introduct*" OR "spread*" OR "expansion" OR "dispers*" OR "range increase")
  AND
      (
        ("invasive" OR "alien" OR "exotic" OR "nonnative" OR "non-native" OR "nonindigenous" OR "non-indigenous")
        NEAR/5 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "rodent$")
      )
)
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))
```


```python
#Termlists
termlist15_8a = ["introduc", "spread", "expansion", "dispers", "range increas",
                 "introduser", "rømme", "forvill", "utvide", "spredning", "sprei", "spre seg", "sprer seg", "spredd seg", "utbre"
                 ]

termlist15_8b = ["invasive","alien","exotic","nonnative","non-native","nonindigenous","non-indigenous",
                  "fremmed"
                 ]

termlist15_8c = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird", "rodent",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl", "gnager",
                 "fremmedart"
                 ]  
                 #"fremmedart"(NO) is added as a term here, as in the trunc list below "art" is not allowed to be truncated. b&c will find "fremmede arter".
                 #This term can be an adjective, or e.g. "fremmedartslista"
termlist15_8c_trunc = ["art", "arter", "dyr"]       

termlist15_8d = ["Pelophylax ridibundus" , "Pelophylax lessonae" , "Pelophylax esculentus" , "Esox lucius" , "Neogobius melanostomus" , "Phoxinus phoxinus" , "Scardinius erythrophthalmus" , "Branta canadensis" , "Barbarea vulgaris" , "Bunias orientalis" , "Elodea canadensis" , "Elodea nuttallii" , "Lactuca serriola" , "Lupinus nootkatensis" , "Symphytum officinale" , "Reynoutria ×bohemica" , "Vincetoxicum rossicum" , "Epilobium ciliatum ciliatum" , "Epilobium ciliatum glandulosum" , "Aruncus dioicus" , "Lamiastrum galeobdolon argentatum" , "Lamiastrum galeobdolon galeobdolon" , "Lysimachia punctata" , "Pastinaca sativa hortensis" , "Amelanchier spicata" , "Berberis thunbergii" , "Cotoneaster bullatus" , "Cotoneaster dielsianus" , "Cotoneaster horizontalis" , "Lonicera caerulea" , "Lysimachia nummularia" , "Rosa rugosa" , "Arctium tomentosum" , "Lupinus polyphyllus" , "Rorippa ×armoracioides" , "Salix viminalis" , "Bromopsis inermis" , "Cerastium tomentosum" , "Cotoneaster lucidus" , "Heracleum mantegazzianum" , "Heracleum persicum" , "Laburnum anagyroides" , "Melilotus albus" , "Petasites japonicus giganteus" , "Petasites hybridus" , "Phedimus spurius" , "Primula elatior elatior" , "Reynoutria sachalinensis" , "Sambucus racemosa" , "Senecio viscosus" , "Sorbaria sorbifolia" , "Swida sericea" , "Vinca minor" , "Taxus ×media" , "Senecio inaequidens" , "Melilotus officinalis" , "Odontites vulgaris" , "Solidago canadensis" , "Festuca rubra commutata" , "Cotoneaster divaricatus" , "Berteroa incana" , "Pinus mugo uncinata" , "Cytisus scoparius" , "Impatiens glandulifera" , "Impatiens parviflora" , "Myrrhis odorata" , "Phedimus hybridus" , "Populus balsamifera" , "Reynoutria japonica" , "Sorbus mougeotii" , "Spiraea ×billardii" , "Spiraea ×rosalba" , "Spiraea ×rubella" , "Tsuga heterophylla" , "Alchemilla mollis" , "Pinus contorta" , "Picea sitchensis" , "Picea ×lutzii" , "Acer pseudoplatanus" , "Laburnum alpinum" , "Pinus mugo" , "Campylopus introflexus" , "Neovison vison" , "Lepus europaeus" , "Nyctereutes procyonoides" , "Sciurus carolinensis" , "Castor canadensis" , "Echinococcus multilocularis" , "Gyrodactylus salaris" , "Angiostrongylus vasorum" , "Anguillicoloides crassus" , "Bursaphelenchus xylophilus" , "Meloidogyne hapla" , "Meloidogyne minor" , "Aphanomyces astaci" , "Batrachochytrium dendrobatidis" , "Batrachochytrium salamandrivorans" , "Hymenoscyphus fraxineus" , "Phytophthora ramorum" , "Phytophthora austrocedri" , "Agrilus planipennis" , "Anoplophora glabripennis" , "Harmonia axyridis" , "Ips amitinus" , "Arion vulgaris" , "Dreissena bugensis" , "Dreissena polymorpha" , "Potamopyrgus antipodarum" , "Opilio canestrinii" , "Eriocheir sinensis" , "Daphnia parvula" , "Pacifastacus leniusculus" , "Aedes japonicus" , "Bombus terrestris" , 
                 "latterfrosk" , "kontinental damfrosk" , "hybridfrosk" , "gjedde" , "svartmunnet kutling" , "ørekyt" , "sørv" , "kanadagås" , "vinterkarse" , "russekål" , "vasspest" , "smal vasspest" , "taggsalat" , "sandlupin" , "valurt" , "hybridslirekne" , "russesvalerot" , "ugrasmjølke" , "alaskamjølke" , "skogskjegg" , "sølvtvetann" , "parkgulltvetann" , "fagerfredløs" , "hagepastinakk" , "blåhegg" , "høstberberis" , "bulkemispel" , "dielsmispel" , "krypmispel" , "blåleddved" , "krypfredløs" , "rynkerose" , "ullborre" , "hagelupin" , "hybridkulekarse" , "kurvpil" , "bladfaks" , "filtarve" , "blankmispel" , "kjempebjørnekjeks" , "tromsøpalme" , "gullregn" , "hvitsteinkløver" , "japanpestrot" , "legepestrot" , "gravbergknapp" , "lundnøkleblom" , "kjempeslirekne" , "rødhyll" , "klistersvineblom" , "rognspirea" , "alaskakornell" , "gravmyrt" , "hybridbarlind" , "boersvineblom" , "legesteinkløver" , "engrødtopp" , "kanadagullris" , "veirødsvingel" , "sprikemispel" , "hvitdodre" , "bergfuru" , "gyvel" , "kjempespringfrø" , "mongolspringfrø" , "spansk kjørvel" , "sibirbergknapp" , "balsampoppel" , "parkslirekne" , "alpeasal" , "klasespirea" , "purpurspirea" , "bleikspirea" , "vestamerikansk hemlokk" , "praktmarikåpe" , "vrifuru" , "sitkagran" , "lutzgran" , "platanlønn" , "alpegullregn" , "alpefuru" , "ribbesåtemose" , "mink " , "sørhare" , "mårhund" , "riebannjáŋkkár" , "furuvednematode" , "askeskuddbeger" , "greindreper" , "asiatisk askepraktbille" , "harlekinmarihøne" , "brunskogsnegl" , "sebramusling" , "vandrepollsnegl" , "gulrotvevkjerring" , "kinaullhåndskrabbe" , "signalkreps" , "mørk jordhumle"
                 ]
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
```
TS=
(
  (
    ("invasive" OR "alien" OR "exotic" OR "nonnative" OR "non-native" OR "nonindigenous" OR "non-indigenous")
    NEAR/3 ("species" OR "flora" OR "fauna" OR "plant$" OR "animal$" OR "organism$" OR "wildlife" OR "insect$" OR "amphibian$" OR "reptile$" OR "bird$" OR "rodent$")
  )
  NEAR/15
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
NOT
TS=(("marine" OR "ocean$" OR "seafloor" OR "coral" OR "kelp forest$" OR "kelp-forest$" OR "random forest$" OR "IOT" OR "urban ecosystem") NOT ("terrestrial" OR "soil" OR "soils" OR "woodland$" OR "taiga" OR "jungle" OR "mangrove$" OR "peatland$" OR "bog$" OR "mire$" OR "fen$" OR "swamp*" OR "wetland$" OR "marsh*" OR "paludal" OR "farmland$" OR "agricultural land$" OR "cropland$" OR "pasture$" OR "rangeland$" OR "bush*" OR "shrub*" OR "meadow*" OR "savanna*" OR "plain$" OR "grassland$" OR "prairie$" OR "dryland$" OR "dry land" OR "desert*" OR "mountain*" OR "highland$" OR "alpine*" OR ("fell$" NEAR/15 "Lapland") OR "tundra" OR "freshwater" OR "limnic" OR "inland fish*" OR "lake*" OR "pond$" OR "river*" OR "stream$" OR "brook$" OR "creek$"))

#Phrase 3
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
                 "reduser", "tiltak", "kontroll", "utrydd", "fjerne", "bekjemp", "spredningshindr", "spreiingshindr", "forebygg", "førebygg"
                 ]

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

```
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

This string has been simplified a bit, as this is complex string for a title search. "Biodiversity" and related terms are used more alone.


```python
#Termlists
termlist15_9a = ["biodiversit","biological diversity", "species diversity",
                 "habitat","biotop",
                 "biologisk diversitet", "biomangf", "artsmangf", "biologisk mangf", "biologiske mangf", "naturmangf",
                 "økosystem", "leveområd",
                 "cbd"]

termlist15_9b = ["community", "environment", "ecosystem", "diversit",
                 "samfunn", "miljø", "mangfold", "mangfald"]
                 #Ecosystem was 50-50 noise, so was moved here to be combined with species, plant etc. 
                 #This phrase is searched for together with 9c, and alone *within* the terrestrial set to find e.g. "forest community"

termlist15_9c = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]

termlist15_9d = ["National biodiversity strategy", "national biodiversity action plan", "national action plan"]
termlist15_9d_case = ["NBSAP"]

termlist15_9e = ["national", "local", "government", "regional", "sector", "municipal", "federal", 
                 "poverty reduction", "reduce poverty", "anti-poverty", "anti poverty",

                 "nasjonal", "regjering", "kommun", "lokal", "fylke", "sektor",
                 "fattigdom"
                 ]
termlist15_9f = ["target", "goal", "program", "strateg", "policy", "policies", "framework", "governance", 
                 "action plan", "development", "accounting", "report",

                 "handlingsplan", "planlegg", "politikk", "retningslin", "rammeverk", "styring", "ledelse", "leiing", "forvaltningsplan", 
                 "utvikling", "rapport"
                 ]
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
    (
        ((Data['result_title'].str.contains(phrasedefault15_9a, na=False, case=False))
        |
          (
             (Data['result_title'].str.contains(phrasedefault15_9b, na=False, case=False))
             & (Data['result_title'].str.contains(phrasedefault15_9c, na=False, case=False))
          )
        )
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_9d, na=False, case=False)) 
            | (Data['result_title'].str.contains(phrasedefault15_9d_case, na=False, case=True))
            |
              (
                  (Data['result_title'].str.contains(phrasedefault15_9e, na=False, case=False))
                  & ((Data['result_title'].str.contains(phrasedefault15_9f, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_9f_trunc, na=False, case=False)))
              )
        )
    )
    &(Data['terrestrial_double_NOT']==True)
),"tempsdg15_09"] = "SDG15_09"

print("Number of results = ", len(Data[(Data.tempsdg15_09 == "SDG15_09")]))  

#search in terr terms
Data.loc[(
    (
        (Data['result_title'].str.contains(phrasedefault15_9b, na=False, case=False))
        & 
        (
            (Data['result_title'].str.contains(phrasedefault15_9d, na=False, case=False)) 
            | (Data['result_title'].str.contains(phrasedefault15_9d_case, na=False, case=True))
            |
              (
                  (Data['result_title'].str.contains(phrasedefault15_9e, na=False, case=False))
                  & ((Data['result_title'].str.contains(phrasedefault15_9f, na=False, case=False))|(Data['result_title'].str.contains(phrasespecific15_9f_trunc, na=False, case=False)))
              )
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


```
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
          ("incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e")
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


```python
#Termlists

termlist15_aa = ["protect","preserv","conserv", "promot", "improv", "restor", 
                 "enhanc", "strengthen", "maintain", "preserv", "support",
                 "verne", "verna", "vern av", "miljøvern", "bevare", "bevaring", "frede", "freda", "fredning", "gjenoppbygg", "restaurer", 
                 "forbedr", "betre", "betring", "styrke", "vedlikeh", "støtte", "stønad"
                 ]

termlist15_ab = ["manag","use","using","govern","development","administrat","planning",
                 "forvalt", "bruk", "styr", "ledelse", "leiing", "utvikl", "planlegg"]
termlist15_ab_trunc = ["use","using",
                       "bruk"]
termlist15_ac = ["sustainabl", "responsib", "environmental", "ecological", "ecosystem",
                 "bærekraft", "berekraft", "ansvarl", "miljø", "økologisk", "økosystem"]

termlist15_ad = ["biodiversit", "biological diversity", "species diversity",
                 "habitat","biotop",
                 "rio marker",
                 "biologisk diversitet", "biomangf", "artsmangf", "biologisk mangf", "biologiske mangf",
                 "økosystem", "leveområd"]

termlist15_ae = ["community", "environment", "ecosystem", "diversit",
                 "samfunn", "miljø", "mangfold"]
                 #Ecosystem was 50-50 noise, so was moved here to be combined with species, plant etc. 
                 #This phrase is searched for together with 9af, and alone *within* the terrestrial set

termlist15_af = ["ecolog", "species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "økologi", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]

termlist15_ag = ["investing", "investment", "investor", "financ", "spending", "funding", "grant", "funds",
                  "incentive", "taxes", "fees", "subsidy", "subsidi",
                  "cooperation fund", "development fund", "development assistance", "international aid", "international assistance", "foreign aid", "foreign assistance", 
                  "global environmental facility", "Biodiversity finance intitiative", 
                  "partnership for action on green economy", 
                  "poverty-environment action for sustainable", "poverty environment action for sustainable",
                  "green commodities program",
                 
                 "finansiel", "midlar", "økonomiske ressurs",
                 "insentiv", "skatt", "subsidier", "subsidiar", "tilskudd", "tilskot",
                 "samarbeidsfond", "utviklingsstøtte", "utviklingsstønad", "bistand", "utviklingshjelp", "u-hjelp"
                 ]
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

Since this is only a title search, we simplify to search for only biodiversity + investment, and dropp the "sustainable use/protect" parts (when used = no results). They are commented-out below.


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
test.iloc[0:5, ]
```

### SDG 15.b

*15.b Mobilize significant resources from all sources and at all levels to finance sustainable forest management and provide adequate incentives to developing countries to advance such management, including for conservation and reforestation*

*Mobilisere betydelige ressurser fra alle kilder og på alle nivåer for å finansiere en bærekraftig skogforvaltning, og sørge for virkemidler som er egnet til å fremme slik forvaltning i utviklingslandene, blant annet virkemidler for bevaring og nyplanting av skog*


#### Phrase 1 & 2
```
#Phrase 1
TS=
(

  ("expenditure" OR "invest" OR "investing" OR "investment$" OR "financ*" OR "spending" OR "funding" OR "funder$" OR "fund$" OR "grant$"
  OR "financial support" OR "financial resources"
  OR "incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
  OR "ODA" OR "cooperation fund$" OR "development spending"
  OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance"))
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

#Phrase 2
TS=
(
  ("expenditure" OR "invest" OR "investing" OR "investment$" OR "financ*" OR "spending" OR "funding" OR "funder$" OR "fund$" OR "grant$"
  OR "financial support" OR "financial resources"
  OR "incentive$" OR "taxes" OR "tax" OR "fees" OR "subsidy" OR "subsidies" OR "subsidi?ing" OR "subsidi?e"
  OR "ODA" OR "cooperation fund$" OR "development spending"
  OR (("international" OR "development" OR "foreign") NEAR/3 ("aid" OR "assistance"))
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
    (****LMICs****
    )
)
```

In this search I have added a NOT search for kelp forest, as there is relatively much about this in Norway and only very rarely is a paper about both terrestrial and kelp forests. 


```python
#Termlists
termlist15_ba = ["investing", "investment", "investor", "financ", "spending", "funding", "grant", "funds",
                  "incentive", "taxes", "fees", "subsidy", "subsidi",
                  "cooperation fund", "development fund", "development assistance", "international aid", "international assistance", "foreign aid", "foreign assistance", 
                 
                 "finansiel", "midlar", "økonomiske ressurs", "økonomiske midler",
                 "insentiv", "skatt", "subsidier", "subsidiar", "tilskudd", "tilskot",
                 "samarbeidsfond", "utviklingsstøtte", "utviklingsstønad", "bistand", "utviklingshjelp", "u-hjelp"
                 ]
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

I suggest simplifying this search, since it is a title search, by only using forests + support. Doing it in this way will also entirely cover any possible results from phrase 2.


```python
#Search 1
Data.loc[(
    ((Data['result_title'].str.contains(phrasedefault15_ba, na=False, case=False)) | (Data['result_title'].str.contains(phrasespecific15_ba_case, na=False, case=True)))
    & (Data['result_title'].str.contains(phrasedefault15_bb, na=False, case=False)) 
    & (~Data['result_title'].str.contains(phrasedefault15_bNOT, na=False, case=False))
),"tempsdg15_b"] = "SDG15_b"

print("Number of results = ", len(Data[(Data.tempsdg15_b == "SDG15_b")]))  
```


```python
test=Data.loc[(Data.tempsdg15_b == "SDG15_b"), ("result_id", "result_title")]
test.iloc[0:5, ]
```

### SDG 15.c
*15.c Enhance global support for efforts to combat poaching and trafficking of protected species, including by increasing the capacity of local communities to pursue sustainable livelihood opportunities*

*Øke den globale støtten til tiltak for å bekjempe krypskyting og ulovlig handel med vernede arter, blant annet ved å styrke lokalsamfunnenes evne til å benytte de muligheter som finnes for å opprettholde et bærekraftig livsgrunnlag*

#### Phrase 1
```
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


```python
#Termlists
termlist15_ca = ["poach", "traffick", "smuggl",
                 "krypskyt", "ulovlig transport", "smugl", "ulovlig", "ulovleg"]

termlist15_cb = ["protected", "endanger", "threat", "extinct", "at risk", "vulnerable", "red list",
                 "truet", "truga", "utryddingstru", "utrydjingstruga", "utsatte", "utsette", "sårbar", "vernet", "verna", "rødlist", "rød list", "raudlist", "raud list"]

termlist15_cc = ["species", "plant", "animal", "organism", "flora", "fauna", "wildlife", "insect", "amphibian", "reptile", "bird",
                 "plant", "rovdyr", "pattedyr", "dyreart", "dyrart", "dyreliv", "insekt", "amfibi", "krypdyr", "fugl"]  
termlist15_cc_trunc = ["art", "arter", "dyr"]                                  

termlist15_cd = ["rosewood" , "kosso" , "elephant" , "rhino" , "ivory" , "pangolin" , "turtle" , "tortoise" , "big cat" , "tiger" , "glass eel",
                 "elefant", "neshorn", "elfenbein", "elfenben", "skilpadde", "store katt", "glassål"
                 "trua arter", "trued art", "truede art"]
                 #"trua arter"(NO) is added as a phrase here since "trua" would be noisy alone

termlist15_ce = ["ended","ending","halted",
                 "resist","reduc","decreas","minimi","tackle","control","prevent","combat",
                 "anti-poaching",
                 "capacity",
                 "cooperation","collaboration","network","support",
                 "policy","policies","empower",
                 "knowledge transfer", "awareness","knowledge", "information", "dissemination",
                 "educat", 
                 "Landscapes for People, Food and Nature partnership",
                 "Convention on International Trade in Endangered Species of Wild",
                 
                 "reduser", "bekjemp", "kontroll", "hindre", "kjempe", "avslutt", 
                 "kapasitet", 
                 "samarbeid", "nettverk", "støtte", "stønad",
                 "politikk", "retningslin", "myndiggjør",
                 "kunnskapsoverfør", "kjenner til", "kunnskap", "informasjon", "formidl",
                 "utdann",
                 "internasjonal handel med truede dyr", "internasjonal handel med truede og sårbare"
                 ]
termlist15_ce_trunc = ["stop","stopping", "end", "ends", "halt",
                      "stoppe"]
termlist15_ce_case = ["CITES"]

phrasedefault15_ca = r'(?:{})'.format('|'.join(termlist15_ca))
phrasedefault15_cb = r'(?:{})'.format('|'.join(termlist15_cb))
phrasedefault15_cc = r'(?:{})'.format('|'.join(termlist15_cc))
phrasedefault15_cc_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_cc_trunc))
phrasedefault15_cd = r'(?:{})'.format('|'.join(termlist15_cd))
phrasedefault15_ce = r'(?:{})'.format('|'.join(termlist15_ce))
phrasedefault15_ce_trunc = r'\b(?:{})\b'.format('|'.join(termlist15_ce_trunc))
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
          |
          (
              (Data['result_title'].str.contains(phrasedefault15_cb, na=False, case=False)) 
              & ((Data['result_title'].str.contains(phrasedefault15_cc, na=False, case=False))|(Data['result_title'].str.contains(phrasedefault15_cc_trunc, na=False, case=False)))
          )
        )
        & (
            (Data['result_title'].str.contains(phrasedefault15_ce, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault15_ce_trunc, na=False, case=False))
            |(Data['result_title'].str.contains(phrasedefault15_ce_case, na=False, case=True))
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
```
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


```python
#Termlists
termlist15_cf = ["Convention on International Trade in Endangered Species of Wild Fauna and Flora",
                 "internasjonal handel med truede dyr", "internasjonal handel med truede og sårbare arter"]
                 #Reuse 15_ce for CITES

termlist15_cg = ["livelihood", "employment",
                 "local communit", "local people", "indigenous communit", "indigenous people", "rural communit", "rural people", "native communit", "native people",
                 "levebrød", "jobb", "tilsatt", "ansatt", "arbeid",
                 "lokale samfunn", "lokalsamfunn", "urfolk", "urbefolkning", "bygd"
                 ]

termlist15_ch = ["sustainab", "ecological", "legal", "alternativ", "eco-friendly", "environmentally friendly",
                 "bærekraft", "berekraft", "økologi", "lovlig", "lovleg", "miljøven", "økoven"
                 ]

termlist15_ci = ["fishing", "fisher", "hunting", "hunter", "touris", "agroforest", "agricult", "income",
                 "fiske", "jakt", "turism", "landbruk", "jordbruk", "inntekt"
                 ]

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
                      |(Data['result_title'].str.contains(phrasedefault15_cc_trunc, na=False, case=False))
                      |(Data['result_title'].str.contains(phrasedefault15_cd, na=False, case=False))
                  )
              )
        )
        & (
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

```
TS=
("SDG 15" OR "SDGs 15" OR "SDG15" OR "sustainable development goal$ 15"
OR ("sustainable development goal$" AND "goal 15")
OR
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 15")
    AND ("life on land")
  )
OR 
  (
    ("sustainable development goal$" OR "SDG$" OR "goal 15")
    NEAR/15 ("mountain$" OR "terrestrial" OR "forest$" OR "dryland$" OR "grassland$")
  )
)
NOT 
  TS=("secoisolariciresinol diglycoside"
  OR "secoisolariciresinol diglucoside"
  OR "SD-stearic acid"
  OR "SD-HPMC"
  OR "short-duration grazing (SDG)"
  OR "short-duration group (SDG)"
  OR "set domain group (SDG)"
  OR "spleen-derived growth factor (SDG)"
  OR "steel design guide series (SDG)"
  OR "steel design guide (SDG)"
  OR "spray-dried gelatin (SDG)"
  OR "single-display groupware (SDG)"
  )
```


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
test=Data.loc[Data['tempsdg03_01'].notna() & Data['tempsdg03_02'].notna()]   
test.iloc[0:4, [1,4,5,6,20,21,23,24,-1, -2, -3]]
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
data2.drop(columns = ["terr_terms", "terrestrial_double_NOT", "marine_terms", "LDCs", "SIDS", "LDS", "LMICs", "LDCSIDS"], inplace=True)
```

### Combined target-level results
This section combines all of the target-level labels. When doing this, we also separate out those that concern the general SDG phrase (i.e. works that mention SDG4 - this is not a target, so we don't want them as a target label)


```python
cols_target_cristin=(data2.filter(like='tempsdg').columns).tolist()
print(type(cols_target_cristin))
```


```python
cols_mentionsthesdg_cristin=(data2.filter(like='tempmentionsdg').columns).tolist()
print(type(cols_mentionsthesdg_cristin))
```


```python
cols_target_cristin
```


```python
cols_mentionsthesdg_cristin
```


```python
# Concatenate the labels for all the target columns
data2['SDG_target_topic_cristin'] = data2[cols_target_cristin].apply(lambda x: x.str.cat(sep=','), axis=1)
#...and all the SDG mention columns
data2['SDG_sdg_topic_cristin'] = data2[cols_mentionsthesdg_cristin].apply(lambda x: x.str.cat(sep=','), axis=1)
```


```python
test=data2.loc[data2['tempsdg03_01'].notna() & data2['tempsdg03_02'].notna()]   
#test=data2.loc[data2['tempmentionsdg02'].notna()]   
test.iloc[0:3, [0,1,4,5,6,20,21,23,24,-1, -2]]
```

### Combined SDG-level results


```python
data2["SDG_topic_cristin"]=""
```


```python
#loop to check whether the target column contains the SDG, and add that SDG to the whole SDG col
SDGlist = ["SDG01", "SDG02", "SDG03", "SDG04", "SDG07", "SDG11", "SDG13", "SDG14", "SDG15"]

for ei in SDGlist:
    data2["SDG_topic_cristin"] = np.where(data2['SDG_target_topic_cristin'].str.contains(ei)|data2['SDG_sdg_topic_cristin'].str.contains(ei), (data2["SDG_topic_cristin"]+","+ei), data2["SDG_topic_cristin"])
```


```python
#Strip beginning comma
data2["SDG_topic_cristin"] = data2["SDG_topic_cristin"].str.lstrip(',')
```


```python
#test
data2.loc[data2.result_id.str.contains("2020739|1796046|1826865|1248913"),].head()
```


```python
#Remove the columns no longer needed
#Remove columns for each individual target...
data2.drop(columns = cols_target_cristin, inplace=True)
#And the columns for the whole sdg searches...
data2.drop(columns = cols_mentionsthesdg_cristin, inplace=True)
data2.drop(columns = "SDG_sdg_topic_cristin", inplace=True)
```

**How many results?**


```python
SDGlist = ["SDG01", "SDG02", "SDG03", "SDG04", "SDG07", "SDG11", "SDG13", "SDG14", "SDG15"]

for ei in SDGlist:
    print("No. results for", (ei), "(topic):", np.count_nonzero(data2['SDG_topic_cristin'].str.contains(ei)))
```


```python
SDGlist = ["SDG03_01", "SDG03_02", "SDG03_03", "SDG03_04"]

for ei in SDGlist:
    print("No. results for", (ei), "(topic):", np.count_nonzero(data2['SDG_target_topic_cristin'].str.contains(ei)))
```

## Final cleaning


```python
# Make a copy of the data
data3=data2.copy()
```


```python
#Clean empty SDG fields to NA
data3.loc[~data3['SDG_target_topic_cristin'].str.contains('SDG'), 'SDG_target_topic_cristin'] = np.nan
data3.loc[~data3['SDG_topic_cristin'].str.contains('SDG'), 'SDG_topic_cristin'] = np.nan
```


```python
data3.info()
```
