# Keeping an item and its information together

## Database integrity, photo retrieval, and publication workflows at Pirages

*David Clark · Portfolio case study · 2 November 2026*

At Phillip J. Pirages Fine Books and Manuscripts, a book's information had to travel through several connected workflows: cataloging, photography, printed catalogues, the company website, and marketplace listings. I inherited an established Access-based environment and worked to improve how those parts stayed connected.

An early problem I found made me aware of the consequences and prompted me to consider whether others existed. A group of leaves had been offered under a single ItemID. When the offering changed to the remaining leaf, the association with its photographs no longer described the same thing. The wrong image became associated with the item. In my July 31, 2009 notes, I recorded the example as `ST11035-6leaves`. That same ItemCode survives in the photo relationship data recovered from an old spreadsheet's pivot cache.

That discovery prompted me to pursue improvements alongside my regular duties. The task extended beyond correcting that one listing: I needed to understand how an item's identity, its changing availability, its catalogue appearances, and its photographs were being represented throughout the system.

### Stable identity across changing presentations

My 2009 email records having to reconcile inconsistent ItemIDs across catalogue rosters, photo associations, the company website data file, AbeBooks and ILAB export files, and the printed catalogues themselves. Changing an identifier in one place could leave several other representations out of step.

I advocated for stable item identifiers and for separating the record of an object from the ways it was advertised. An item could appear in multiple catalogues or offerings; a photograph could be reused; a group could be broken into individual offerings. The database needed to represent those relationships as distinct links between records. My earlier experience at Harrison House/ECI had shown me how changing ItemIDs could disrupt sales history, returns, and other connected records. That experience informed my approach at Pirages: changing an ItemID to accommodate a new presentation made its history harder to follow.

I also identified the limitations of the inherited `Alpha` field: a text field whose codes and notes controlled catalogue section and order while also carrying status, location, task notes, and other operational information. It was useful to the staff who understood its conventions, but it was difficult to reuse consistently in queries and reports. My proposed restructuring gave distinct kinds of information their own fields.

### Making the photograph relationships usable

I built `Photos.mdb`, an Access photo database, to index and retrieve image files, using hyperlinks in forms to bring the photographs into view. The original Access file has not been recovered. A surviving spreadsheet cache preserves a substantial portion of the item–photo relationships, however, including fields I remember creating for that work.

| Surviving field | Role in the workflow |
| --- | --- |
| `ItemCode` | Identifies the inventory item represented in the relationship. |
| `PhotoID` | Identifies an image within the catalogue-based naming system. Lettered variants can identify crops derived from a group photograph. It does not establish the item's latest catalogue appearance. |
| `ItemPhotoPlace` | Identifies which object is meant when a photograph contains several items, read left to right and top to bottom. |
| `WebUse` | Flags the primary image selected to represent an item on the website. The old site could display only one photograph per listing. |
| `ItemPhotoCount` | Numbers the photographs associated with an item, distinguishing them and showing how many are available. These can include photographs in which the item appears alongside other items. |
| `Alpha` | Carries inherited sorting and operational information associated with the item. |

The recovered dataset contains **6,816 relationship rows, 2,282 distinct ItemCodes, and 4,753 distinct PhotoIDs**. These are different measures: one item can have several photographs, and one photograph can represent several items. There are 1,185 rows flagged `WebUse = TRUE`; that is a count within the historical cache, rather than a count of currently published web images.

For example, `ST11458` has 13 linked image records, with one flagged for web use. The records include a group photograph and a crop derived from it, so they do not represent 13 separate camera exposures. Selecting a primary photograph gave each item a chosen image to represent it online. The old website could display only that one photograph. A primary image also serves search results and landing pages on a site that offers additional photographs within each entry. The surviving data makes the distinction between the available photographs and the selected listing image visible.

### Preserving the connection between a group photograph and its crops

An item could have several photographs of its own and also appear alongside other items in a group photograph. Cropping that group created another image to track. I retained the group PhotoID as the basis for the cropped versions and added letter suffixes to distinguish them.

The surviving records for `56E0174` show how these relationships worked together:

| PhotoID | ItemCode | ItemPhotoPlace | ItemPhotoCount | Meaning in this example |
| --- | --- | --- | --- | --- |
| 56E0174 | ST11458 | 1 | 12 | First item in the group |
| 56E0174 | ST11416 | 2 | 1 | Second item in the group |
| 56E0174 | ST10942 | 3 | 5 | Third item in the group |
| 56E0174a | ST11458 | 1 | 13 | Crop of the first item |
| 56E0174b | ST11416 | 1 | 2 | Crop of the second item |
| 56E0174c | ST10942 | 1 | 6 | Crop of the third item |

Each crop resets `ItemPhotoPlace` to 1 because it now shows its own item. `ItemPhotoCount` belongs to the item's set of linked images: the same group photograph is number 12 for one item, number 1 for another, and number 5 for the third. The suffix connects the derived image to its source, while the item relationship places it within that object's photographic record.

`ST11458` is the Book of Hours offered as item 445 in Cat 60: an illuminated manuscript in Latin and French, Use of Amiens, circa 1450, priced at $110,000. It contains 13 miniatures, including small narrative scenes in the lower borders, and it appeared on the front cover and Plates 28–29. That range of material helps explain why the item had so many images available for selection.

A wider examination of the recovered cache found 510 group PhotoIDs with single-letter variants. Of 2,063 variants examined, 2,050 link to one item from the original group and place that item at position 1. In 2,043 of those cases, the letter also corresponds to its original numbered position. This pattern supports the crop interpretation, while the exceptions show why the actual item relationships still matter. One ItemCode can occupy several positions in a group, for example, and more than one crop can therefore belong to the same item.

In `54E0020`, for example, `ST11221km` occupies positions 1 and 2, while `ST11221j` occupies position 3. The derived images `54E0020a` and `54E0020b` both link to `ST11221km`; `54E0020c` links to `ST11221j`. Two crops can therefore represent different views or components of one inventory item.

### Keeping the image aligned with the offering

I remember cropping group photographs when some of the pictured items had sold or would not appear in the next catalogue. The purpose was to avoid showing unavailable or omitted companions in a way that could confuse the reader. Reusing an existing photograph also avoided having to arrange another shoot when a suitable crop would do the job.

There was another option in the earlier plate workflow: we could retain the group photograph and replace an item's number beneath it with a bold **SOLD** caption. That kept the rest of the photograph useful while making the change in availability clear. I associate this practice with larger manuscript-leaf groups, which could contain seven or more items. Smaller groups and the increasing use of photographs beside individual entries reduced the need for this treatment. The exact transition date remains uncertain.

These were publication decisions as well as image-editing decisions. The system needed to preserve what an image showed, which item a crop represented, and which version had been chosen for a particular use.

### Preparing exports and checking what happened afterward

The July 2009 email lists queries I had created or modified in `Piragescom.mdb`, with instructions for using them. They covered full uploads, incremental updates, photo selection, and comparison of marketplace data with the current inventory state.

Examples include `qPhotoIDWebUse`, for selected web PhotoIDs; `qPhotoWebList`, for the current catalogues' web photographs and the list used to copy files to a website staging area; and `qPiragesWebUpload`, which used a replacement function to prepare the description markup for HTML output. Other queries checked listings against the `Alpha` field to find sold, subsumed, or missing items.

Each destination imposed different requirements. My notes document differences in quotation handling, price formats, and image support, including the delay before marketplace changes could be inspected. Preparing the export and checking its published result were both part of the work.

### Preparing photographs for future catalogue use

As I improved the photography setup, I also changed how I approached photographs taken for customer requests and other immediate needs. Earlier ad hoc photographs had been taken with a less expensive camera and without the same preparation. After I upgraded the equipment and added LED display lighting, I aimed to make every photograph suitable for catalogue use.

That gave catalogue preparation a growing supply of usable images. I provided Phil with a report or contact sheet so that he could review what was available and request supplementary photographs. In my recollection, this approach substantially reduced the additional photography needed just before production.

### What the work demonstrates

This project connected practical database work with analysis of how the business operated. I investigated errors across systems, built and modified queries, developed a photo retrieval workflow, and proposed changes where inherited structures made the information difficult to maintain.

The surviving material supports both the operational work and the reasoning behind it. The named queries are described in a contemporary email as created or modified; the photo associations survive as data; and the wider redesign is documented as a set of proposals. Together, they show how I approached a fragmented workflow by tracing relationships and building checks around them.


---

[Sources and evidence boundaries](SOURCE_GUIDE.md)
