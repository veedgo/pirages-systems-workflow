# Sources and evidence boundaries

## Contemporary documentation

- David Clark, **Website and Database update copy off site**, July 31, 2009. The full message documents upload/comparison queries, the ST11035-6leaves association problem, and proposed restructuring. The appended third-party article is excluded from attribution to Clark. Original query SQL has not been recovered.
- **FW: Addressing website database issues**, forwarded June 22, 2010, containing David's June 9 outline and Jenny's June 11 responses. Supports collaborative requirements gathering. Jenny's replies remain her contribution; the correspondence does not prove delivery of the proposed replacement system.
- **FW: Announcement: Portland InDesign User Group Meeting, September 8th**, August 17, 2011. David connected database-to-layout automation research with his current work. Attendance and use of a particular plugin are unconfirmed.
- **Designing electronic versions of the Call Form and Master catalog and other database updating**, March 18, 2014. Distinguishes existing tables from a proposed Call Forms table and records a Bibliopolis inquiry. Completion of electronic call forms is unconfirmed.

The private correspondence is described here as evidence; full messages and personal addresses are not distributed with this package.

## Recovered relationship data

**Pirages_PivotCache_Flattened.xlsx** is a modern recovery artifact derived from a historical workbook cache. It contains 6,816 relationship rows, 2,282 distinct ItemCodes, and 4,753 distinct PhotoIDs. Its historical snapshot date is unconfirmed and is not assigned the July 2009 email date.

Selected CSVs preserve five original fields: ItemCode, PhotoID, ItemPhotoPlace, WebUse, and ItemPhotoCount. The operational Alpha field is omitted. TRUE/FALSE values describe the historical selection, not current availability. Image records include derived crops and must not be counted as separate camera exposures.

The suffix analysis examined base IDs matching two digits, E or P, and four digits, with at least two distinct linked ItemCodes and at least one single-letter lowercase variant. It found 510 bases and 2,063 variants. Of those variants, 2,050 link to exactly one source-group ItemCode and have position 1 throughout; 2,043 also match the corresponding original position. This is an analysis of names and recorded relationships, not visual examination of the original photographs.

## Published catalogue

**Phillip J. Pirages, Catalogue 60**, item 445, PDF pages 181-182, identifies ST11458 as a Book of Hours, Use of Amiens, circa 1450. It records a $110,000 asking price, 13 miniatures, and references to the front cover and Plates 28-29. The miniature count and image-record count are separate measures.

## Firsthand recollection

David Clark identifies ItemPhotoPlace, WebUse, and ItemPhotoCount as fields he created. His explanations establish the form hyperlinks, crop workflow, use of SOLD captions, improvements to photography/lighting, and contact-sheet review with Phil. Photos.mdb follows his recollection; the contemporary email uses Photo.mdb. The original filename remains unverified.

The reason and timing of particular crops are not encoded in the cache. A specific SOLD caption beneath a group photograph has not been located. The draft describes a gradual reduction in the usefulness of group captions without fixing a catalogue boundary. No automatic sales-driven cropping or caption-generation process is claimed.

## Reconstruction and implementation

The diagram explains relationships inferred from surviving fields and firsthand explanations. It is not an original Access schema. The original .mdb files and forms remain unavailable. Complete separation of Alpha and completion of the wider redesign are not established.

## Credits

Portfolio narrative and professional experience: David Clark. Historical catalogue descriptions and original catalogue material: Phillip J. Pirages Fine Books and Manuscripts and their credited contributors. Data recovery, analysis, and exhibit preparation were assisted by ChatGPT/Codex in 2026.
