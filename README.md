# Polybius Tutorial: Telling the Story of the Medici Antiquities Network

## Introduction

This tutorial walks you through building a complete scrollytelling data story using Polybius. By the end, you will have a multi-section narrative about Giacomo Medici's illicit antiquities trafficking network that uses every visualization type Polybius offers: timelines, maps, network graphs, statistical charts, image galleries, single images, and text-only narrative cards.

The dataset is drawn from Neil Brodie's entry in the [Trafficking Culture Project case study encyclopedia on Giacomo Medici](https://traffickingculture.org/encyclopedia/case-studies/giacomo-medici/), which itself draws on published investigative journalism and court records. Some rows are narrative events; others carry explicit financial values for charting. This mix is intentional — in Polybius, different rows can serve different visualization purposes within the same CSV.

Open [Polybius](https://shawngraham.github.io/polybius) in a new window.

To view the results of this tutorial, [see the resulting site here](https://shawngraham.github.io/polybius-demo).

---

## Part 1: Preparing Your Data
## 1.1 The CSV file

Save the following as medici.csv. It contains 37 rows covering events, people, objects, transactions, and legal actions spanning 1960–2011.

```csv
id,label,date,latitude,longitude,category,description,connections,imageUrl,value,object_type,source
M1,Giacomo Medici begins dealing in Rome,1960,41.9028,12.4964,Dealer Activity,"Medici starts dealing in antiquities in Rome during the 1960s, entering the illicit trade network at its Italian source.","M12,M13,M14,M15,",https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,0,event,Silver 2009: 25
M2,Medici convicted of receiving looted artefacts,1967,41.9028,12.4964,Legal Action,"In July 1967 Medici is convicted in Italy of receiving looted artefacts. In the same year he meets US dealer Robert Hecht, who becomes a key buyer.",,https://upload.wikimedia.org/wikipedia/commons/a/ab/Colosseo_di_Roma_panoramic.jpg,1,event,Silver 2009: 27-9
M3,Antiquaria Romana gallery opens in Rome,1968,41.9028,12.4964,Dealer Activity,Medici opens the gallery Antiquaria Romana in Rome and begins exploring business opportunities in Switzerland.,,https://upload.wikimedia.org/wikipedia/commons/2/25/Piazza_Navona_1.jpg,0,event,Silver 2009: 34
M4,Euphronios (Sarpedon) krater acquired,1971,41.9028,12.4964,Key Object,Medici is widely believed to have bought the illegally-excavated Euphronios krater from tombaroli before transporting it to Switzerland and selling it to Robert Hecht.,,https://upload.wikimedia.org/wikipedia/commons/5/59/Euphronios_krater_side_A_MET_L.2006.10.jpg,1000000,event,Silver 2009: 50
M5,Partnership with Christian Boursaud begins,1978,46.2044,6.1432,Dealer Activity,"Medici closes his Rome gallery and enters into partnership with Geneva-based Christian Boursaud, who starts consigning Medici's material for sale at Sotheby's London.",,https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,0,event,"Silver 2009: 121-2, 139"
M6,Hydra Gallery opens in Geneva,1983,46.2044,6.1432,Dealer Activity,Medici and Boursaud open the Hydra Gallery in Geneva. Throughout the 1980s Medici becomes the single largest source of consignments to Sotheby's London.,,https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,500000,event,Silver 2009: 139; Watson and Todeschini 2007: 27
M7,Sotheby's London consignments peak,1985,51.5074,-0.1278,Auction House,At any one time Boursaud might consign up to seventy objects worth as much as £500000 to Sotheby's London. Material is delivered from Geneva by courier.,,https://upload.wikimedia.org/wikipedia/commons/b/be/Sotheby%27s_%2851921999492%29.jpg,500000,event,Watson 1997: 112
M8,Onesimos kylix sold to J. Paul Getty Museum,1985,34.0259,-118.4739,Key Object,In October 1985 the Hydra Gallery sells fragments of the Onesimos kylix to the Getty for $100000 with a false provenance via the fictitious Zbinden collection. The Getty returns the kylix to Italy in 1999.,,https://upload.wikimedia.org/wikipedia/commons/b/b8/Getty_Center_2.jpg,100000,object,Silver 2009: 145; Watson and Todeschini 2007: 95
M9,Editions Services acquired,1986,46.2044,6.1432,Dealer Activity,Bad publicity over looted Apulian vases causes Medici and Boursaud to part company. Medici buys Geneva-based Editions Services to continue consigning material to Sotheby's.,,https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,0,event,Silver 2009: 147; Watson and Todeschini 2007: 27
M10,Front companies used for triangulation,1987,46.2044,6.1432,Laundering Method,From 1987 to 1994 Medici consigns through front companies Mat Securitas Arts Franc and Tecafin Fiduciaire. He develops a triangulation system to create artificial demand and launder stolen objects with a Sotheby's provenance.,"M35,",https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,0,method,Watson and Todeschini 2007: 73
M11,Network of major dealers established,1989,46.2044,6.1432,Network,Medici develops commercial relations with Robin Symes Frieda Tchacos Nikolas Koutoulakis Robert Hecht and Ali and Hicham Aboutaam.,"M12,M13,M14,M15,",https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,0,event,Watson and Todeschini 2007: 73-4
M12,Robin Symes,1989,51.5074,-0.1278,Dealer,"London-based antiquities dealer and key Medici client, handled onward sales to collectors and museums.","M1,M11,M16,M17,",,0,person,Watson and Todeschini 2007: 73-4
M13,Frieda Tchacos,1989,46.2044,6.1432,Dealer,Geneva-based antiquities dealer linked to Medici's supply network.,"M1,M11,",,0,person,Watson and Todeschini 2007: 73-4
M14,Robert Hecht,1989,48.8566,2.3522,Dealer,Paris-based American dealer. Medici's earliest major buyer dating to 1967. Later prosecuted in Italy.,"M1,M2,M4,M11,M29,M30,",https://upload.wikimedia.org/wikipedia/commons/a/ac/La_Tour_Eiffel_vue_de_la_Tour_Saint-Jacques%2C_Paris_ao%C3%BBt_2014.jpg,0,person,Watson and Todeschini 2007: 73-4
M15,Ali and Hicham Aboutaam,1989,46.2044,6.1432,Dealer,Geneva-based brothers and antiquities dealers connected to Medici's distribution chain.,"M1,M11,",,0,person,Watson and Todeschini 2007: 73-4
M16,Sales to private collectors,1989,40.7128,-74.006,Collector,Medici is the ultimate source of artefacts sold to collectors including the Fleischmans Maurice Tempelsman Shelby White and Leon Levy the Hunt brothers George Ortiz and José Luis Várez Fisa.,"M12,",https://upload.wikimedia.org/wikipedia/commons/3/30/Metropolitan_Museum_of_Art_%28The_Met%29_-_Central_Park%2C_NYC.jpg,0,event,Watson and Todeschini 2007: 112-34; Isman 2010
M17,Sales to major museums,1989,40.7128,-74.006,Museum,Museums receiving Medici-sourced artefacts include the J. Paul Getty the Metropolitan Museum of Art the Cleveland Museum of Art and the Boston Museum of Fine Arts.,"M8,M12,M23,M30,M31,",https://upload.wikimedia.org/wikipedia/commons/3/30/Metropolitan_Museum_of_Art_%28The_Met%29_-_Central_Park%2C_NYC.jpg,0,event,Watson and Todeschini 2007: 112-34
M18,Stolen sarcophagus identified at Sotheby's,1995,51.5074,-0.1278,Legal Action,A Sotheby's London auction catalogue advertises a sarcophagus recognized by the Carabinieri as stolen from the church of San Saba in Rome. Sotheby's reveals it was consigned by Editions Services.,,https://upload.wikimedia.org/wikipedia/commons/b/be/Sotheby%27s_%2851921999492%29.jpg,0,event,Watson and Todeschini 2007: 19
M19,Organigram discovered,1995,41.9028,12.4964,Legal Action,Italian investigators discover the organigram revealing Medici's central position in the organisation of the antiquities trade out of Italy.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,0,event,Watson and Todeschini 2007: 19
M20,Geneva Freeport raided,1995,46.2044,6.1432,Legal Action,On 13 September 1995 Carabinieri and Swiss police raid Medici's five-room storage space in the Geneva Freeport covering about 200 sq metres. One room is a restoration lab another a showroom.,,https://upload.wikimedia.org/wikipedia/commons/5/50/Lighthouse_Switzerland-02549_-_Les_Paquis_Lighthouse_%2823248580962%29.jpg,3800,event,Silver 2009: 174; Watson and Todeschini 2007: 20
M21,Medici arrested in Rome,1997,41.9028,12.4964,Legal Action,In January 1997 Medici is arrested in Rome. In July 1997 the sealed Geneva storerooms are reopened for examination and inventory.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,0,event,Silver 2009: 175-6
M22,Freeport inventory completed,1999,46.2044,6.1432,Legal Action,The official report lists 3800 whole or fragmentary objects more than 4000 photographs and 35000 sheets of paper. Artefacts are mainly from Italy but also from Egypt Syria Greece and Asia. Photographs show objects in stages of restoration some still covered in excavation dirt.,,https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,3800,event,Silver 2009: 192
M23,Getty returns Onesimos kylix to Italy,1999,34.0259,-118.4739,Repatriation,The J. Paul Getty Museum returns the Onesimos kylix to Italy following acknowledgement of its illicit origins.,,https://upload.wikimedia.org/wikipedia/commons/1/15/Getty_Center_2.jpg,100000,object,Silver 2009: 145; Watson and Todeschini 2007: 95
M24,Santa Marinella home raided,2002,42.0333,11.85,Legal Action,Carabinieri raid Medici's home in Santa Marinella finding additional evidence.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,0,event,Watson and Todeschini 2007: 200
M25,Trial begins in Rome,2003,41.9028,12.4964,Legal Action,Medici's trial on charges of receiving stolen goods illegal export and conspiracy to traffic commences on 4 December 2003 in Rome.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,0,event,Silver 2009
M26,Medici convicted on all charges,2005,41.9028,12.4964,Legal Action,On 12 May 2005 Medici is found guilty of all charges. The judge declares he trafficked thousands of artefacts including the San Saba sarcophagus and the Euphronios krater. He is sentenced to ten years in prison and a €10 million fine.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,10000000,event,Silver 2009: 212-14
M27,Appeals court reduces sentence,2009,41.9028,12.4964,Legal Action,An appeals court dismisses the trafficking conviction due to an expired limitation period but reaffirms receiving and conspiracy convictions. The sentence is reduced to eight years but the €10 million fine stands.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,10000000,event,Scherer 2009
M28,Final appeal fails,2011,41.9028,12.4964,Legal Action,A further appeal fails. Medici's convictions for receiving stolen goods and conspiracy are upheld.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,10000000,event,Felch 2012
M29,Marion True and Robert Hecht prosecuted,2005,41.9028,12.4964,Legal Action,Evidence from the Medici investigation triggers the prosecutions of former Getty curator Marion True and dealer Robert Hecht in Italian courts.,,https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,0,event,Watson and Todeschini 2007
M30,Euphronios (Sarpedon) krater,1971,41.9028,12.4964,Key Object,Red-figure calyx-krater painted by Euphronios depicting the death of Sarpedon. Illegally excavated from a Cerveteri tomb and sold through Hecht to the Metropolitan Museum of Art for $1 million in 1972. Returned to Italy in 2008.,"M4,M14,M17,M26,",https://upload.wikimedia.org/wikipedia/commons/5/59/Euphronios_krater_side_A_MET_L.2006.10.jpg,1000000,object,Silver 2009: 50
M31,Onesimos kylix,1985,34.0259,-118.4739,Key Object,Attic red-figure kylix attributed to Onesimos. Sold to the J. Paul Getty Museum for $100000 via the Hydra Gallery with a fabricated Zbinden provenance. Returned to Italy in 1999.,"M8,M17,M23,",https://upload.wikimedia.org/wikipedia/commons/b/b8/Getty_Center_2.jpg,100000,object,Silver 2009: 145; Watson and Todeschini 2007: 95
M32,San Saba sarcophagus fragment,1995,51.5074,-0.1278,Key Object,Roman sarcophagus fragment stolen from the church of San Saba in Rome. Consigned to Sotheby's London through Editions Services. Its identification in the 1995 auction catalogue triggered the Medici investigation. Estimated value £50000.,"M18,M26,",https://upload.wikimedia.org/wikipedia/commons/b/be/Sotheby%27s_%2851921999492%29.jpg,50000,object,Watson and Todeschini 2007: 19
M33,Apulian vases (Sotheby's consignment),1986,51.5074,-0.1278,Key Object,Group of looted Apulian red-figure vases consigned to Sotheby's London. The bad publicity surrounding their sale ended the Medici-Boursaud partnership. Estimated combined lot value £200000.,"M5,M9,",https://upload.wikimedia.org/wikipedia/commons/b/be/Sotheby%27s_%2851921999492%29.jpg,200000,object,Silver 2009: 147; Watson and Todeschini 2007: 27
M34,Typical Boursaud-era Sotheby's consignment,1984,51.5074,-0.1278,Transaction,Representative single consignment batch: up to seventy objects worth as much as £500000 delivered from Geneva to Sotheby's London by courier.,"M5,M7,",https://upload.wikimedia.org/wikipedia/commons/b/be/Sotheby%27s_%2851921999492%29.jpg,500000,transaction,Watson 1997: 112
M35,Triangulated auction purchase (front company),1990,46.2044,6.1432,Transaction,Typical triangulation deal: object consigned through one front company and bought back through another to create artificial demand and launder provenance via a Sotheby's sale record. Estimated average lot value £75000.,"M10,",https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,75000,transaction,Watson and Todeschini 2007: 135-41
M36,Freeport inventory — objects,1999,46.2044,6.1432,Transaction,3800 whole or fragmentary antiquities recovered from the Geneva Freeport storerooms. Conservatively valued at an average of €5000 per piece giving total estimated stock value of €19 million.,"M20,M22,",https://upload.wikimedia.org/wikipedia/commons/2/26/Geneva-aerial-view.JPG,19000000,transaction,Silver 2009: 192; Watson and Todeschini 2007: 54-68
M37,Court-imposed fine,2005,41.9028,12.4964,Transaction,€10 million fine imposed on conviction as compensation to the Italian state for damage to cultural heritage. Upheld on appeal in 2009.,"M26,M27,M28,",https://upload.wikimedia.org/wikipedia/commons/6/6e/Roma_-_Piazza_San_Pietro_-_Basilica_di_San_Pietro_-_panoramio.jpg,10000000,transaction,Silver 2009: 214
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
|`connections`|	Comma-separated IDs linking rows to each other|	Network graph|
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
