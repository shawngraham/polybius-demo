# Polybius Tutorial: Telling the Story of the Medici Antiquities Network

## Introduction

This tutorial walks you through building a complete scrollytelling data story using Polybius. By the end, you will have a multi-section narrative about Giacomo Medici's illicit antiquities trafficking network that uses every visualization type Polybius offers: timelines, maps, network graphs, statistical charts, image galleries, single images, and text-only narrative cards.

The dataset is drawn from Neil Brodie's entry in the [Trafficking Culture Project case study encyclopedia on Giacomo Medici](https://traffickingculture.org/encyclopedia/case-studies/giacomo-medici/), which itself draws on published investigative journalism and court records. Some rows are narrative events; others carry explicit financial values for charting. This mix is intentional — in Polybius, different rows can serve different visualization purposes within the same CSV.

Open [Polybius](https://shawngraham.github.io/polybius) in a new window.

To view the results of this tutorial, [see the resulting site here](https://shawngraham.github.io/polybius-demo).

Note that the current version of Polybius *might* have slightly different interface configuration options, but this is more or less how it goes. Also, you can now embed a youtube or vimeo video in a 'text' card, just by putting the link in the historical chronicle box.

---

## Part 1: Preparing Your Data
## 1.1 The CSV file

Save the following as medici.csv. It contains 37 rows covering events, people, objects, transactions, and legal actions spanning 1960–2011.

```csv
id,label,date,latitude,longitude,category,connections,description,imageUrl,value
M01,Giacomo Medici,1967,41.9,12.5,Dealer,M02;M03;M04;M05;M06;M07;M08;M11;M12;M24,Italian antiquities dealer active from the 1960s. Convicted in 2005 of receiving stolen goods and conspiracy to traffic. Central node in one of the largest illicit antiquities networks ever uncovered.,https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Roma_piazza_navona.jpg/800px-Roma_piazza_navona.jpg,
M02,Robert Hecht,1967,40.71,-74,Dealer,M01;M09;M14;M17,US-based antiquities dealer who purchased material from Medici from 1967 onward. Believed to have acquired the Euphronios krater from Medici in 1971 and sold it to the Metropolitan Museum.,https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Metropolitan_Museum_of_Art_%28The_Met%29_-_Central_Park%2C_NYC.jpg/800px-Metropolitan_Museum_of_Art_%28The_Met%29_-_Central_Park%2C_NYC.jpg,
M03,Christian Boursaud,1978,46.2,6.14,Dealer,M01;M10;M12,Geneva-based partner of Medici from 1978. Consigned Medici's material to Sotheby's London and co-founded the Hydra Gallery in 1983. Partnership dissolved in 1986.,https://upload.wikimedia.org/wikipedia/commons/thumb/2/28/Jet_d%27Eau_de_Gen%C3%A8ve.jpg/800px-Jet_d%27Eau_de_Gen%C3%A8ve.jpg,
M04,Robin Symes,1988,51.51,-0.13,Dealer,M01,London-based antiquities dealer who developed commercial relations with Medici by the late 1980s.,https://upload.wikimedia.org/wikipedia/commons/thumb/c/cd/London_Montage_L.jpg/800px-London_Montage_L.jpg,
M05,Frieda Tchacos,1988,47.37,8.54,Dealer,M01,Dealer with commercial relations with Medici by the late 1980s. Part of the network identified through the Freeport evidence.,https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Zurich_Fraumunster_Grossmunster.jpg/800px-Zurich_Fraumunster_Grossmunster.jpg,
M06,Nikolas Koutoulakis,1988,48.86,2.35,Dealer,M01,Paris-based antiquities dealer connected to Medici's supply network by the late 1980s.,https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/Tour_Eiffel_Wikimedia_Commons.jpg/800px-Tour_Eiffel_Wikimedia_Commons.jpg,
M07,Ali Aboutaam,1988,46.2,6.14,Dealer,M01;M08,Geneva-based dealer and brother of Hicham Aboutaam. Developed commercial relations with Medici by the late 1980s.,https://upload.wikimedia.org/wikipedia/commons/thumb/2/28/Jet_d%27Eau_de_Gen%C3%A8ve.jpg/800px-Jet_d%27Eau_de_Gen%C3%A8ve.jpg,
M08,Hicham Aboutaam,1988,40.71,-74,Dealer,M01;M07,New York-based dealer and brother of Ali Aboutaam. Part of Medici's downstream distribution network.,https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Southwest_corner_of_Central_Park%2C_looking_east%2C_NYC.jpg/800px-Southwest_corner_of_Central_Park%2C_looking_east%2C_NYC.jpg,
M09,Marion True,1985,34.01,-118.5,Curator,M02;M13,Former antiquities curator at the J. Paul Getty Museum. Her prosecution was triggered by evidence recovered during the Medici investigation.,https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/J._Paul_Getty_Museum.jpg/800px-J._Paul_Getty_Museum.jpg,
M10,Sotheby's London,1978,51.53,-0.14,Auction House,M03;M11;M21,Throughout the 1980s Medici was the source of more consignments to Sotheby's London than any other vendor. Material delivered from Geneva by courier.,https://upload.wikimedia.org/wikipedia/commons/b/be/Sotheby%27s_%2851921999492%29.jpg,500000
M11,Editions Services,1986,46.2,6.14,Front Company,M01;M10;M21,Geneva-based company purchased by Medici in 1986 to continue consigning material to Sotheby's after his split with Boursaud.,https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Geneva-Freeport-20091011.jpg/800px-Geneva-Freeport-20091011.jpg,
M12,Hydra Gallery,1983,46.2,6.14,Gallery,M01;M03;M13;M18,Gallery opened in Geneva in 1983 by Medici and Boursaud. Sold the Onesimos kylix fragments to the Getty in 1985 using a false provenance.,https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,500000
M13,J. Paul Getty Museum,1985,34.01,-118.5,Museum,M09;M12;M18,Purchased the Onesimos kylix from Hydra Gallery in 1985 for $100000. Returned the kylix to Italy in 1999 and later the Aphrodite of Morgantina.,https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/J._Paul_Getty_Museum.jpg/800px-J._Paul_Getty_Museum.jpg,
M14,Metropolitan Museum of Art,1972,40.78,-73.96,Museum,M02;M17,Acquired the Euphronios krater in 1972 via Hecht. The krater was displayed for over 30 years before being returned to Italy in 2008.,https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Metropolitan_Museum_of_Art_%28The_Met%29_-_Central_Park%2C_NYC.jpg/800px-Metropolitan_Museum_of_Art_%28The_Met%29_-_Central_Park%2C_NYC.jpg,
M15,Cleveland Museum of Art,1990,41.51,-81.61,Museum,M01,Among the museums found to have acquired material ultimately sourced from Medici's network.,https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Cleveland_Museum_of_Art_%2823380172750%29.jpg/800px-Cleveland_Museum_of_Art_%2823380172750%29.jpg,
M16,Boston Museum of Fine Arts,1990,42.34,-71.09,Museum,M01,Among the museums found to have acquired material ultimately sourced from Medici's network.,https://upload.wikimedia.org/wikipedia/commons/thumb/b/bb/Museum_of_Fine_Arts_Boston.jpg/800px-Museum_of_Fine_Arts_Boston.jpg,
M17,Euphronios Krater,1971,42,12.1,Object,M01;M02;M14,Illegally excavated near Cerveteri c.1971. Believed purchased by Medici from tombaroli then sold to Hecht then to the Met for $1 million. Returned to Italy 2008.,https://upload.wikimedia.org/wikipedia/commons/5/59/Euphronios_krater_side_A_MET_L.2006.10.jpg,1000000
M18,Onesimos Kylix,1985,34.01,-118.5,Object,M12;M13,Fragments sold by Hydra Gallery to the Getty in 1985 for $100000 with a false provenance citing the fictitious Zbinden collection. Returned to Italy 1999.,https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/J._Paul_Getty_Museum.jpg/800px-J._Paul_Getty_Museum.jpg,100000
M19,Geneva Freeport,1995,46.21,6.13,Location,M01;M20,Medici's five-room storage space raided 13 September 1995. Found to contain 3800 artefacts and over 4000 Polaroid photographs documenting looted objects.,https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Geneva-Freeport-20091011.jpg/800px-Geneva-Freeport-20091011.jpg,3800
M20,Carabinieri TPC,1995,41.9,12.5,Law Enforcement,M19;M21;M01,Italy's cultural property protection unit. Coordinated with Swiss police on the 1995 Freeport raid. Recovered the organigram and thousands of Polaroids.,https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/CoA_Arma_dei_Carabinieri.svg/800px-CoA_Arma_dei_Carabinieri.svg.png,
M21,San Saba Sarcophagus,1995,41.88,12.49,Object,M11;M10;M20,Sarcophagus stolen from the church of San Saba in Rome. Recognized in a 1995 Sotheby's catalogue consigned by Editions Services. Triggered the Medici investigation.,https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Basilica_di_San_Saba_-_panoramio.jpg/800px-Basilica_di_San_Saba_-_panoramio.jpg,
M22,Shelby White & Leon Levy,1988,40.71,-74,Collector,M01,New York-based private collectors identified as recipients of material ultimately sourced from Medici.,https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Southwest_corner_of_Central_Park%2C_looking_east%2C_NYC.jpg/800px-Southwest_corner_of_Central_Park%2C_looking_east%2C_NYC.jpg,
M23,Fleischman Collection,1988,34.05,-118.24,Collector,M01,Lawrence and Barbara Fleischman were private collectors identified as recipients of material ultimately sourced from Medici.,https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Griffith_Observatory_-_Dusk.jpg/800px-Griffith_Observatory_-_Dusk.jpg,
M24,Antiquaria Romana,1968,41.9,12.5,Gallery,M01,Gallery opened by Medici in Rome in 1968. Closed in 1978 when Medici moved his operations to Switzerland.,https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Roma_piazza_navona.jpg/800px-Roma_piazza_navona.jpg,
M25,Medici convicted on all charges,2005,41.9028,12.4964,DEALER,,On 12 May 2005 Medici is found guilty of all charges. The judge declares he trafficked thousands of artefacts including the San Saba sarcophagus and the Euphronios krater. He is sentenced to ten years in prison and a €10 million fine.,,10000000
```

## 1.2 Understanding the columns

|Column|	Purpose|	Used by|
|------|---------|---------|
|`id`|	Unique row identifier|  	All views (internal)|
|`label`|	Display name shown on markers, nodes, tooltips|	All views|
|`date`|	Year of event|	Timeline, Line chart X axis|
|`latitude` / `longitude`|	Geographic coordinates|	Map|
|`category`|	Thematic grouping (Legal Action, Dealer Activity, Key Object, etc.)|	Bar chart, color coding|
|`description`|	Long-form text for tooltips and galleries	|All views|
|`connections`|	Semi-comma-separated IDs linking rows to each other|	Network graph|
|`imageUrl`|	Image URL	(in this case, to Wikimedia Commons) | Gallery, Single Image |
|`value`|	Monetary figure in the transaction's original currency |	Line chart Y axis, XY scatter, 3D bubble |
|`object_type`|	Secondary grouping (event, person, object, transaction, method) |	Bar chart alternative grouping |
|`source`|	Bibliographic citation|	Text narrative reference|

Notice that not every row is useful to every visualization. The `person` rows (M12–M15) have no meaningful `value` but are essential for the network graph. The `Transaction` rows (M34–M37) exist primarily to feed the charts. This is normal — a single CSV powers many views, and each view draws on the columns it needs.

---

## Part 2: Loading the Data

1. Open Polybius. It loads by default the sample Silk Road dataset. You can delete the individual cards for this by clicking on the trash icons. You can also reset Polybius to the default by clicking the **New Project** button (trash icon in the toolbar) and confirm to clear everything you've changed.

2. Click the **Dataset** tab (the page icon) in the left sidebar.

3. Click **Upload CSV** and select your `medici.csv` file. You should see all 37 rows loaded, with column headers `id`, `label`, `date`, `latitude`, `longitude`, `category`, `description`, `connections`, `imageUrl`, `value`, `object_type`, `source`.

---

## Part 3: Setting Up Metadata

Click the **Settings** tab (gear icon) in the left sidebar.

Fill in the fields:
|Field	|Value|
|-------|-----|
|**Title**|	The Medici Network |
|**Subtitle**|	Anatomy of an Illicit Antiquities Trafficking Operation|
|**Author**|	_(your name)_ |
|**Collaborators**|	_(optional)_|

These values appear in the header of the exported site. If you later choose the **Playful** theme, the title will also ghost into the background as a subtle text effect.

## 3.1 Adding bibliography entries

Still in the Settings tab, scroll down to **Bibliography**. Click **Add Entry** for each source and enter:

+ `Brodie, Neil. nd. 'Giacomo Medici'. _Trafficking Culture Project_ `
+ `Silver, Vernon. 2009. The Lost Chalice. New York: William Morrow.`
+ `Watson, Peter. 1997. Sotheby's: The Inside Story. London: Bloomsbury.`
+ `Watson, Peter and Cecilia Todeschini. 2007. The Medici Conspiracy. New York: PublicAffairs.`
+ `Isman, Fabio. 2010. I predatori dell'arte perduta. Milan: Skira.`

These will render as a bibliography section at the bottom of the exported site.

---

## Part 4: Building the Sections

Click the **Content** tab (the layout icon). You will build ten sections. For each one, click **Add Section**, then configure it as described below.

**Section 1 — Introduction (Text Only)**

|Setting	| Value|
|----|----|
|**Section Heading**	|The Corrosion of Cultural Heritage|
|**Visualization Type**	|Text Only|
|**Card Alignment**	|Full|
|**Text Alignment**|	Justify|

**Historical Chronicle** (paste into the text area):
>In 2005, an Italian court convicted Giacomo Medici of receiving stolen goods, illegal export, and conspiracy to traffic in illicit antiquities. The verdict was the culmination of a decade-long investigation that revealed a sophisticated transnational network connecting Italian tomb robbers to the world's most prestigious museums and private collections. This data story traces the geographic, financial, and interpersonal contours of that network — from Medici's first dealings in 1960s Rome, through the Swiss freeport warehouses, London auction rooms, and American museum boardrooms, to the courtroom where the system was finally exposed.

**Why Text Only?** This opening section has no visualization — it sets the scene. The `full` card alignment makes it span the entire width of the screen rather than sitting in the left column, giving it the weight of an opening statement.

**Section 2 — Timeline of Events**

|Setting|	Value|
|---|---|
|**Section Heading**|	Five Decades of Trafficking|
|**Visualization Type**	|Timeline View|
|**Card Alignment**	|Left|

Under **Mapping & Constraints**:

|Setting|	Value|
|---|---|
|**Display Label**	|`label`|
|**Date Column**	|`date`|

**Historical Chronicle**:
> The timeline below spans from 1960, when Medici first began dealing in Rome, through 2011 when his final appeal was rejected. Notice the long latency between criminal activity and legal consequence — nearly three decades separate his first conviction in 1967 from the Freeport raid in 1995. The clustering of events in the mid-1990s marks the moment when Italian and Swiss authorities finally coordinated action.

**What you'll see**: A timeline with all 37 rows ordered by year. Events cluster visibly around 1985–1995 (peak activity) and 1995–2005 (investigation and prosecution).

You can set the timeline to render horizontally or vertically.

**Section 3 — Geographic Spread**

|Setting|	Value|
|---|---|
|**Section Heading**|	A Continental Operation|
|**Visualization Type**	|Geographic Map|
|**Card Alignment**	|Left|

Under **Mapping & Constraints**:

|Setting|	Value|
|---|---|
|**Display Label**	|`label`|
|**Latitude**	|`latitude`|
|**Longitude**|	`longitude`|
|**Base Map**	|`Watercolour`|

**Historical Chronicle**:
> The map reveals the geographic architecture of Medici's network. Rome was the source — where tombaroli extracted objects from Etruscan and Roman sites. Geneva was the laundry — where objects were cleaned, restored, documented, and given fictitious provenances in the tax-free environment of the Freeport. London was the marketplace — where Sotheby's provided the veneer of legitimate auction provenance. And the terminal destinations were American museums and private collections in New York and Los Angeles. Hover over the markers to see what happened at each location.

**What you'll see**: Markers in Rome, Geneva, London, Paris, New York, Los Angeles, and Santa Marinella. The spatial triangle of Rome–Geneva–London is immediately legible.

You can set the zoom level and the starting map centre in the editor.

**Section 4 — The Network**

|Setting	|Value|
|---|---|
|**Section Heading**	|The Web of Complicity|
|**Visualization Type**|	Network Graph|
|**Card Alignment**	|Left|

Under **Mapping & Constraints**:

|Setting |Value|
|---|---|
|**Display Label**	|`label`|
|**Connections**|	`connections`|

**Historical Chronicle**:
> The network graph visualizes the connections column in the dataset. Each node is an event, person, or object; each edge represents a documented relationship. Medici sits at the centre of a hub-and-spoke structure — he is connected, directly or through intermediaries, to every major dealer, museum, and collector in the network. The 'organigram' seized by Italian investigators in 1995 mapped exactly this structure. Notice how the Euphronios krater (M4/M30) connects Medici to Hecht, the Metropolitan Museum, and ultimately to the investigation that brought the network down.

**What you'll see**: A force-directed graph. Medici-related event nodes (M1, M4, M5, M11) form dense hubs. Dealer nodes (M12–M15) radiate outward. Museum and collector nodes (M16, M17) sit at the periphery — the end of the supply chain.

**Section 5 — Key Object: The Euphronios Krater**

|Setting |Value|
|---|---|
|**Section Heading**	|The Smoking Gun|
|**Visualization Type**	|Single Image|
|**Card Alignment**|	Left|

Under **Mapping & Constraints**:

|Setting|	Value|
|---|---|
|**Image URL Column**	|`imageUrl`|
|**Description Column**	|`description`|
|**Display Label**	|`label`|
|**Item Number**	|M4|

**Historical Chronicle**:
> No single object better illustrates the mechanics of the illicit trade than the Euphronios krater. Painted around 515 BCE by the artist Euphronios and depicting the death of Sarpedon, it was illegally excavated from a tomb near Cerveteri in late 1971. Medici purchased it from tombaroli, transported it to Switzerland, and sold it to Robert Hecht, who then sold it to the Metropolitan Museum of Art in New York for one million dollars — at the time, the most expensive antiquity ever purchased. The krater remained at the Met for thirty-six years before being returned to Italy in 2008. It was central evidence in Medici's trial.

**Why Item Number 30**? The `Item Number` field (1-indexed) tells Polybius which row in the dataset to display. Row 30 is M30, the dedicated Euphronios krater object record with its image and description.

**Section 6 — Financial Scale (Bar Chart)**

|Setting|Value|
|---|---|
|**Section Heading**	|Following the Money|
|**Visualization Type**	|Statistical Chart|
|**Card Alignment**|	Left|

Under **Mapping & Constraints**:

|Setting	|Value|
|---|---|
|**Chart Type**|	`Bar Chart`|
|**Display Label**	|`label`|
|**Category / Group By**|	`category`|

**Historical Chronicle**:
> This bar chart groups the 37 events by category. The dominance of 'Legal Action' reflects how thoroughly the investigative and judicial process has been documented — nine separate legal milestones, from the 1967 conviction through the 2011 final appeal. The 'Dealer Activity' category captures the business infrastructure Medici built across three decades. 'Key Object' entries represent specific looted antiquities whose journeys from tomb to museum have been reconstructed. Note that 'Transaction' rows are synthetic summaries included to carry financial values for the charts that follow.

**What you'll see**: A bar chart with bars for each `category` value. Legal Action is the tallest bar. This gives a structural overview of the dataset itself — what kinds of evidence exist about the Medici network.

**Section 7 — Value Over Time (Line Chart)**

|Setting	|Value|
|---|---|
|**Section Heading**	|The Escalating Stakes|
|**Visualization Type**	|Statistical Chart|
|**Card Alignment**	|Left|

Under **Mapping & Constraints**:

|Setting|	Value|
|---|---|
|**Chart Type**|	`Line Chart`|
|**Display Label**|	`label`|
|**X Axis (numeric)**|	`date`|
|**Y Axis Columns**	|click `value` to select it|

**Historical Chronicle**:
>The line chart plots monetary value against time. The early spike in 1971 marks the Euphronios krater ($1 million). The mid-1980s see sustained high values — the Sotheby's consignment batches averaging £500,000 each and the $100,000 Onesimos kylix sale to the Getty. Values drop in the early 1990s as the front-company triangulation deals carry smaller individual amounts. Then the chart spikes dramatically in 1999 (the estimated €19 million Freeport inventory) and 2005 (the €10 million court fine). The financial trajectory mirrors the narrative arc: gradual escalation, peak activity, and then a reckoning measured in the same currency as the crimes.

**What you'll see**: A line with peaks at 1971, 1984–1985, 1999, and 2005. The 1999 Freeport inventory value dominates the chart. Rows with `value: 0` (narrative events without financial figures) sit at the baseline — they don't distort the chart, they simply don't contribute to it.

**Section 8 — Scatter Plot: Dates vs Values**

|Setting	|Value|
|---|---|
|**Section Heading**|	Objects, Transactions, Penalties|
|**Visualization Type**|	Statistical Chart|
|**Card Alignment**|	Left|

Under **Mapping & Constraints**:

|Setting	|Value|
|---|---|
|**Chart Type**|	`XY Scatter`|
|**Display Label**	|`label`|
|**X Axis**	|`date`|
|**Y Axis**	|`value`|

**Historical Chronicle**:
> The scatter plot shows each row as a point positioned by date and value. Most narrative rows cluster along the bottom at zero — they carry no financial information and are included for the timeline, map, and network views. The financially significant data points float above: the krater at 1971, the consignment batches in the 1980s, the freeport valuation and the court fine. This view makes clear something important about our data: the quantitative and qualitative records serve different analytical purposes, and a single dataset can support both modes of inquiry. The absence of value data is itself meaningful — it marks where the documentary record captures events but not prices.

**Section 9 — Image Gallery**

|Setting	|Value|
|---|---|
|**Section Heading**	|Places in the Network|
|**Visualization Type**	|Image Gallery|
|**Card Alignment**|	Left|

Under **Mapping & Constraints**:

|Setting	|Value|
|---|---|
|**Display Label**|	`label`|
|**Image URL Column**	|`imageUrl`|
|**Description Column**|	`description`|

**Historical Chronicle**:
> The gallery draws on the imageUrl column to display location photographs associated with each event. While these are modern images of the cities involved — Rome, Geneva, London, Paris, New York, Los Angeles — they give spatial texture to the network. The Getty Center in Los Angeles, Sotheby's on New Bond Street in London, the aerial views of Geneva where the Freeport warehouses held thousands of looted objects: these places are not incidental to the story. They are the institutional infrastructure that made the trade possible.

**Section 10 — Conclusion (Text Only)**

|Setting	|Value|
|---|---|
|**Section Heading**	|What the Data Shows|
|**Visualization Type**	|Text Only|
|**Card Alignment**|	Full|
|**Text Alignment**	|Justify|

**Historical Chronicle**:
> The Medici case is not merely a story about one man. The network graph shows a system — a supply chain with specialized roles at every stage: extraction (tombaroli), consolidation (Medici), laundering (Geneva Freeport and Sotheby's auction provenances), distribution (dealers like Symes, Hecht, Tchacos, and the Aboutaams), and acquisition (museums and private collectors). The financial data shows that this system moved millions of dollars in cultural property over decades. The timeline shows that it took institutional will — coordinated action by the Carabinieri and Swiss police — to disrupt what market incentives alone could not. The geographic map shows that the system exploited jurisdictional boundaries: objects crossed from Italy to Switzerland to England to the United States precisely because each border crossing made legal accountability harder. These are not four separate stories. They are four views of the same structure, told through the same data.

**Text Card Feature**
Polybius checks the text in the 'chronicle' section in text cards to auto-detect YouTube and Vimeo URLs in the narrative content and render them as responsive 16:9 iframe embeds. Polybius supports youtube.com/watch?v=, youtu.be/, and vimeo.com/ URL formats. Non-video text around the URLs renders normally

---

## Part 5: Choosing a Theme

Click the **Visual Aesthetic** tab (palette icon). Eight themes are available:
|Theme	|Character	|Good for|
|---|---|---|
|Classic|	Clean, modern, neutral	|General-purpose presentations
Parchment|	Warm, serif, archival|	Historical and humanities content
Academic|	High contrast, structured	|Formal publications
Dark|	Dark background, light text	|Atmospheric narratives
High| Contrast	Black on white, WCAG AAA	|Accessibility requirements
Maritime|	Deep navy, gold accents|	Maritime or colonial history
Forest|	Earthy greens, warm stone|	Environmental or rural topics
Playful	|Dark purple, ghosted title	| Investigative, conspiratorial, inviting discovery

For this dataset, **Playful** or **Dark** work well. The Playful theme ghosts the site title ("The Medici Network") into the background of the header at very low opacity, layered at different sizes and slight rotations — it creates the feeling of being let in on a secret, which suits investigative content about hidden networks.

**Parchment** is also a strong choice if you want the content to feel more like a historical research article.

Select a theme and click **Preview** to see it applied. If the preview doesn't update, click **Preview** again (it forces a full refresh).

---

## Part 6: Previewing and Exporting

Click the **Preview** button in the top toolbar. The right panel shows your scrollytelling site. Scroll through it to verify each section renders correctly.

If you need to make changes, click **Editor** to return, make your edits, then click **Preview** again.

When satisfied, click the **Download** button (the download icon in the toolbar). Polybius generates a single standalone HTML file containing all your data, configuration, and visualizations. No server is needed — the file can be opened directly in any browser or hosted on any static file server (GitHub Pages, Netlify, an institutional web server, etc.).

The exported file is fully responsive. On desktop, the scrollytelling layout uses a left-column narrative with a sticky right-column visualization. On mobile devices, visualizations render inline below each narrative card.

If you have python installed on your local computer, you can open a terminal in the unzipped folder and start a web server with `python -m http.server 8000` and your site will be viewable at `localhost:8000`.

---    

## Part 7: Tips for Extending This Project

**Adding more objects**. The Medici investigation identified thousands of trafficked artefacts. You could add rows for specific objects returned by the Getty, the Met, or the Boston MFA, each with their own `value`, `date`, and `connections` entries. The network graph and charts will incorporate them automatically.

**Using `object_type` as an alternative grouping**. Try creating a second bar chart section with **Category / Group By** set to `object_type` instead of `category`. This gives you bars for `event`, `person`, `object`, `transaction`, and `method` — a different analytical lens on the same data.

**3D Bubble chart**. Add a section with **Chart Type** set to **3D Bubble**, X axis as `date`, Y axis as `value`, and Z axis (size) as another numeric column. If you add a column counting the number of `connections` per row, that would size bubbles by network centrality — the Euphronios krater and the Freeport raid would appear as the largest bubbles.

**Filtering rows**. Polybius currently visualizes all rows in every section. If you want a chart that only shows `Key Object` rows, you would create a separate CSV containing just those rows and load it as a second project. Alternatively, structure your narrative sections to guide the reader's attention to specific data points within the full dataset.
