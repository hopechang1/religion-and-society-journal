# Instructions: Converting Academic Journal Article PDFs to TEI P5 XML

These instructions guide the conversion of scanned or digital PDF journal articles into valid TEI P5-conformant XML files. Follow each section in order.

---

## Step 1: Extract and Prepare the Text

1. If the PDF is a **digital PDF** (selectable text), copy the full text directly.
2. If the PDF is a **scanned image**, use an OCR tool (e.g., Tesseract, Adobe Acrobat) to extract the text before proceeding.
3. Note all structural features of the article: title, author(s), editor(s), footnotes, section headings, page breaks, foreign-language passages, and bibliographic details.
4. Record the full **source publication metadata**: journal title, volume, issue, article number, page range, publisher, place of publication, and date.

---

## Step 2: Set Up the XML File

Open a new file with the `.xml` extension. Begin with the following two processing instructions, which declare the TEI schema for validation:

```xml
<?xml-model href="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei_all.rng" type="application/xml" schematypens="http://relaxng.org/ns/structure/1.0"?>
<?xml-model href="http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei_all.rng" type="application/xml" schematypens="http://purl.oclc.org/dml/ns/structure/1.0"?>
<TEI xmlns="http://www.tei-c.org/ns/1.0">
```

---

## Step 3: Encode the `<teiHeader>`

The `<teiHeader>` is divided into several child elements. Follow the structure and internal comment formatting below exactly.

### 3.1 Overall Header Structure

```xml
<teiHeader>

    <!-- Mandatory -->
    <fileDesc> ... </fileDesc>

    <!-- Optional but recommended -->
    <encodingDesc> ... </encodingDesc>

    <!-- Optional -->
    <profileDesc> ... </profileDesc>

    <!-- Optional but highly recommended -->
    <revisionDesc> ... </revisionDesc>

</teiHeader>
```

---

### 3.2 `<fileDesc>` — File Description (Mandatory)

`<fileDesc>` has three mandatory children: `<titleStmt>`, `<publicationStmt>`, and `<sourceDesc>`. `<editionStmt>` is optional but recommended.

```xml
<!-- Mandatory -->
<fileDesc>

    <titleStmt>

        <title>Electronic edition of "[ARTICLE TITLE]" ([JOURNAL], [YEAR], volume [N], issue [N], article [N])</title>

        <author>[ARTICLE AUTHOR FULL NAME]</author>

        <editor>[VOLUME/ISSUE EDITOR FULL NAME]</editor>

        <respStmt>
            <resp>First digitization process led by</resp>
            <name>[NAME]</name>
            <name>[NAME]</name>
            <name>[NAME]</name>
        </respStmt>

        <respStmt>
            <resp>XML encoded by</resp>
            <name>[NAME OR ORGANIZATION]</name>
        </respStmt>

        <respStmt>
            <resp>Browser Display designed by</resp>
            <name>[NAME]</name>
        </respStmt>

        <respStmt>
            <resp>Encoded by</resp>
            <name>[NAME]</name>
        </respStmt>

        <respStmt>
            <resp>Revised by</resp>
            <name>[NAME AND TEAM, IF APPLICABLE]</name>
        </respStmt>

        <funder>[FUNDING INSTITUTION 1]</funder>
        <funder>[FUNDING INSTITUTION 2]</funder>

        <sponsor>[DESCRIPTION OF GRANT OR SPONSORSHIP]</sponsor>

    </titleStmt>

    <!-- Optional but recommended -->
    <editionStmt>

        <edition>[PROJECT NAME] edition <date when="[YYYY-MM-DD]">[WRITTEN OUT DATE]</date></edition>

        <respStmt>
            <resp>First digitization by</resp>
            <name>[INSTITUTION]</name>
        </respStmt>

        <respStmt>
            <resp>Revised and TEI P5-conform encoding by</resp>
            <name>[INSTITUTION OR LAB]</name>
        </respStmt>

    </editionStmt>

    <!-- Mandatory -->
    <publicationStmt>

        <publisher>[PUBLISHER OF DIGITAL EDITION, or "tbd"]</publisher>
        <pubPlace>[PLACE OF DIGITAL PUBLICATION, or "tbd"]</pubPlace>
        <distributor>[DISTRIBUTOR, or "tbd"]</distributor>
        <date>[YEAR OF DIGITAL PUBLICATION]</date>

        <availability>
            <p>[COPYRIGHT AND RIGHTS STATEMENT]</p>
        </availability>

    </publicationStmt>

    <!-- Mandatory -->
    <sourceDesc>

        <biblStruct>

            <analytic>
                <author>[ARTICLE AUTHOR FULL NAME]</author>
                <title>[ARTICLE TITLE IN ORIGINAL LANGUAGE]</title>
            </analytic>

            <monogr>
                <title>[JOURNAL TITLE]</title>
                <editor>[EDITOR OF JOURNAL VOLUME/ISSUE]</editor>

                <respStmt>
                    <resp>Contributor</resp>
                    <name>[CONTRIBUTOR NAME]</name>
                    <name>[CONTRIBUTOR NAME]</name>
                    <name>[CONTRIBUTOR NAME]</name>
                </respStmt>

                <imprint>
                    <pubPlace>[ORIGINAL PLACE OF PUBLICATION]</pubPlace>
                    <publisher>[ORIGINAL PUBLISHER]</publisher>
                    <date>[ORIGINAL YEAR OF PUBLICATION]</date>
                    <biblScope unit="volume">[VOLUME NUMBER]</biblScope>
                    <biblScope unit="issue">[ISSUE NUMBER]</biblScope>
                    <biblScope unit="article">[ARTICLE NUMBER]</biblScope>
                    <biblScope unit="page" from="[START PAGE]" to="[END PAGE]"/>
                </imprint>

            </monogr>

        </biblStruct>

    </sourceDesc>

</fileDesc>
```

---

### 3.3 `<encodingDesc>` — Encoding Description (Optional but Recommended)

```xml
<!-- Optional but highly recommended -->
<encodingDesc>

    <projectDesc>
        <p>[BRIEF STATEMENT OF THE PROJECT'S PURPOSE]</p>
    </projectDesc>

    <samplingDecl>
        <p>[CRITERIA FOR WHAT WAS INCLUDED OR EXCLUDED FROM THE TEXT]</p>
    </samplingDecl>

    <editorialDecl>
        <p>[DESCRIPTION OF HOW THE TEXT WAS EDITED DURING DIGITIZATION]</p>
    </editorialDecl>

</encodingDesc>
```

---

### 3.4 `<profileDesc>` — Profile Description (Optional)

Use `<langUsage>` to declare all languages present in the document. Use ISO 639-2/B language codes (e.g., `eng`, `ger`, `lat`, `fre`).

```xml
<!-- Optional -->
<profileDesc>

    <langUsage>
        <language ident="[ISO-CODE]">[LANGUAGE NAME]</language>
        <language ident="[ISO-CODE]">[LANGUAGE NAME]</language>
    </langUsage>

</profileDesc>
```

---

### 3.5 `<revisionDesc>` — Revision Description (Optional but Highly Recommended)

List changes in **reverse chronological order** (most recent first).

```xml
<!-- Optional but highly recommended -->
<revisionDesc>

    <listChange>
        <change when="[YYYY-MM-DD]">[DESCRIPTION OF MOST RECENT CHANGE]</change>
        <change when="[YYYY-MM-DD]">[DESCRIPTION OF EARLIER CHANGE]</change>
        <change notAfter="[YYYY-MM-DD]">[DESCRIPTION OF EARLIEST/ORIGINAL VERSION]</change>
    </listChange>

</revisionDesc>
```

Use `notAfter` (instead of `when`) for the earliest change when the exact date is uncertain.

---

## Step 4: Encode the `<text>` Body

After the `</teiHeader>` closing tag, add the article's text content inside a `<text>` element.

```xml
<text>
    <body>

        <div type="article">

            <head>[ARTICLE TITLE]</head>

            <!-- Use <p> for paragraphs -->
            <p>[PARAGRAPH TEXT]</p>

            <!-- Use <pb> to mark original page breaks -->
            <pb n="[PAGE NUMBER]"/>

            <!-- Use <div type="section"> for named sections with headings -->
            <div type="section">
                <head>[SECTION HEADING]</head>
                <p>[PARAGRAPH TEXT]</p>
            </div>

            <!-- Use <note place="bottom"> for footnotes -->
            <note place="bottom" n="[FOOTNOTE NUMBER]">[FOOTNOTE TEXT]</note>

            <!-- Use <foreign xml:lang="[ISO-CODE]"> for non-primary-language passages -->
            <foreign xml:lang="lat">[LATIN TEXT]</foreign>

            <!-- Use <hi rend="italic"> for italicized text -->
            <hi rend="italic">[ITALICIZED TEXT]</hi>

            <!-- Use <hi rend="bold"> for bolded text -->
            <hi rend="bold">[BOLD TEXT]</hi>

            <!-- Use <quote> for block quotations -->
            <quote>
                <p>[QUOTED TEXT]</p>
            </quote>

            <!-- Use <bibl> for inline bibliographic references -->
            <bibl>[BIBLIOGRAPHIC REFERENCE]</bibl>

        </div>

    </body>
</text>
```

---

## Step 5: Close the Document

```xml
</TEI>
```

---

## Step 6: Validate the File

1. Open the completed `.xml` file in an XML-aware editor such as **oXygen XML Editor** or **VS Code** with the XML extension.
2. Validate against the TEI All schema declared in the processing instructions at the top of the file.
3. Resolve any schema errors before finalizing the file.
4. Add a `<change>` entry to `<revisionDesc>` recording the date of validation.

---

## Quick Reference: Common TEI P5 Elements

| Element | Use |
|---|---|
| `<p>` | Paragraph |
| `<pb n="N"/>` | Page break (with original page number) |
| `<lb/>` | Line break |
| `<head>` | Heading of a `<div>` |
| `<div type="...">` | Structural division (article, section, etc.) |
| `<note place="bottom">` | Footnote |
| `<foreign xml:lang="...">` | Text in a foreign language |
| `<hi rend="italic">` | Italic text |
| `<hi rend="bold">` | Bold text |
| `<quote>` | Block quotation |
| `<bibl>` | Bibliographic reference |
| `<title>` | Title (within `<bibl>` or header) |
| `<author>` | Author name |
| `<date when="YYYY-MM-DD">` | Date with machine-readable attribute |
| `<persName>` | Personal name mentioned in text |
| `<placeName>` | Place name mentioned in text |

---

## Notes on Language and Transcription

- Preserve the **original spelling and orthography** of the source text, including archaic or non-standard forms.
- Do **not** silently correct OCR errors; mark uncertain readings with `<unclear>` and guesses with `<supplied>`.
- For passages damaged or illegible in the source, use `<gap reason="illegible"/>`.
- Encode all **footnotes** present in the original, preserving their numbering.
