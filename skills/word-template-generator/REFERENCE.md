# WordprocessingML Reference

Complete XML reference for generating Word documents (.docx) using direct OOXML manipulation.

## Table of Contents

1. [Document Structure](#document-structure)
2. [Paragraphs](#paragraphs)
3. [Runs and Text Formatting](#runs-and-text-formatting)
4. [Tables](#tables)
5. [Lists and Numbering](#lists-and-numbering)
6. [Styles](#styles)
7. [Headers and Footers](#headers-and-footers)
8. [Hyperlinks](#hyperlinks)
9. [Images](#images)
10. [Fields](#fields)
11. [Section Properties](#section-properties)
12. [Element Reference Tables](#element-reference-tables)

---

## Document Structure

### Basic Document (word/document.xml)

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<w:document xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"
    xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships">
    <w:body>
        <!-- All content goes here -->

        <!-- Section properties must be last in body -->
        <w:sectPr>
            <w:pgSz w:w="12240" w:h="15840"/>
            <w:pgMar w:top="1440" w:right="1440" w:bottom="1440" w:left="1440" w:header="720" w:footer="720"/>
        </w:sectPr>
    </w:body>
</w:document>
```

### Page Sizes (w:pgSz)

| Size | Width (twips) | Height (twips) |
|------|---------------|----------------|
| Letter | 12240 | 15840 |
| A4 | 11906 | 16838 |
| Legal | 12240 | 20160 |
| A5 | 8391 | 11906 |

---

## Paragraphs

### Basic Paragraph

```xml
<w:p>
    <w:r>
        <w:t>Plain text paragraph</w:t>
    </w:r>
</w:p>
```

### Paragraph with Properties

```xml
<w:p>
    <w:pPr>
        <w:pStyle w:val="Heading1"/>
        <w:jc w:val="center"/>
        <w:spacing w:before="240" w:after="120"/>
    </w:pPr>
    <w:r>
        <w:t>Centered heading with spacing</w:t>
    </w:r>
</w:p>
```

### Paragraph Alignment (w:jc)

```xml
<w:jc w:val="left"/>      <!-- Left aligned (default) -->
<w:jc w:val="center"/>    <!-- Centered -->
<w:jc w:val="right"/>     <!-- Right aligned -->
<w:jc w:val="both"/>      <!-- Justified -->
```

### Paragraph Spacing (w:spacing)

```xml
<w:spacing
    w:before="240"          <!-- Space before in twips (12pt = 240) -->
    w:after="120"           <!-- Space after in twips -->
    w:line="276"            <!-- Line height (276 = 1.15 spacing) -->
    w:lineRule="auto"/>     <!-- auto | exact | atLeast -->
```

### Paragraph Indentation (w:ind)

```xml
<w:ind
    w:left="720"            <!-- Left indent in twips (0.5") -->
    w:right="720"           <!-- Right indent -->
    w:firstLine="360"       <!-- First line indent -->
    w:hanging="360"/>       <!-- Hanging indent (for lists) -->
```

### Paragraph Borders (w:pBdr)

```xml
<w:pBdr>
    <w:top w:val="single" w:sz="4" w:space="1" w:color="000000"/>
    <w:bottom w:val="single" w:sz="4" w:space="1" w:color="2E74B5"/>
    <w:left w:val="single" w:sz="4" w:space="4" w:color="000000"/>
    <w:right w:val="single" w:sz="4" w:space="4" w:color="000000"/>
</w:pBdr>
```

### Paragraph Shading (w:shd)

```xml
<w:shd w:val="clear" w:color="auto" w:fill="FFFF00"/>  <!-- Yellow background -->
```

### Tab Stops (w:tabs)

```xml
<w:tabs>
    <w:tab w:val="left" w:pos="720"/>      <!-- Left tab at 0.5" -->
    <w:tab w:val="center" w:pos="4320"/>   <!-- Center tab at 3" -->
    <w:tab w:val="right" w:pos="8640"/>    <!-- Right tab at 6" -->
    <w:tab w:val="decimal" w:pos="5760"/>  <!-- Decimal tab -->
</w:tabs>
```

---

## Runs and Text Formatting

### Basic Run

```xml
<w:r>
    <w:t>Text content</w:t>
</w:r>
```

### Run with Formatting

```xml
<w:r>
    <w:rPr>
        <w:b/>                              <!-- Bold -->
        <w:i/>                              <!-- Italic -->
        <w:u w:val="single"/>               <!-- Underline -->
        <w:sz w:val="24"/>                  <!-- 12pt (half-points) -->
        <w:color w:val="FF0000"/>           <!-- Red text -->
        <w:rFonts w:ascii="Arial" w:hAnsi="Arial"/>
    </w:rPr>
    <w:t>Formatted text</w:t>
</w:r>
```

### Preserve Whitespace

```xml
<w:t xml:space="preserve">  Text with spaces  </w:t>
```

### Multiple Runs in One Paragraph

```xml
<w:p>
    <w:r>
        <w:rPr><w:b/></w:rPr>
        <w:t>Bold text</w:t>
    </w:r>
    <w:r>
        <w:t xml:space="preserve"> followed by </w:t>
    </w:r>
    <w:r>
        <w:rPr><w:i/></w:rPr>
        <w:t>italic text</w:t>
    </w:r>
</w:p>
```

### Line Break

```xml
<w:r>
    <w:t>First line</w:t>
</w:r>
<w:r>
    <w:br/>
</w:r>
<w:r>
    <w:t>Second line</w:t>
</w:r>
```

### Page Break

```xml
<w:p>
    <w:r>
        <w:br w:type="page"/>
    </w:r>
</w:p>
```

### Tab Character

```xml
<w:r>
    <w:tab/>
</w:r>
```

---

## Tables

### Basic Table

```xml
<w:tbl>
    <w:tblPr>
        <w:tblW w:w="5000" w:type="pct"/>  <!-- 100% width -->
    </w:tblPr>
    <w:tblGrid>
        <w:gridCol w:w="4320"/>
        <w:gridCol w:w="4320"/>
    </w:tblGrid>
    <w:tr>
        <w:tc>
            <w:p><w:r><w:t>Cell 1</w:t></w:r></w:p>
        </w:tc>
        <w:tc>
            <w:p><w:r><w:t>Cell 2</w:t></w:r></w:p>
        </w:tc>
    </w:tr>
</w:tbl>
```

### Table with Borders

```xml
<w:tblPr>
    <w:tblW w:w="5000" w:type="pct"/>
    <w:tblBorders>
        <w:top w:val="single" w:sz="4" w:space="0" w:color="000000"/>
        <w:left w:val="single" w:sz="4" w:space="0" w:color="000000"/>
        <w:bottom w:val="single" w:sz="4" w:space="0" w:color="000000"/>
        <w:right w:val="single" w:sz="4" w:space="0" w:color="000000"/>
        <w:insideH w:val="single" w:sz="4" w:space="0" w:color="000000"/>
        <w:insideV w:val="single" w:sz="4" w:space="0" w:color="000000"/>
    </w:tblBorders>
</w:tblPr>
```

### Table without Borders (Layout Table)

```xml
<w:tblPr>
    <w:tblW w:w="5000" w:type="pct"/>
    <w:tblBorders>
        <w:top w:val="nil"/>
        <w:left w:val="nil"/>
        <w:bottom w:val="nil"/>
        <w:right w:val="nil"/>
        <w:insideH w:val="nil"/>
        <w:insideV w:val="nil"/>
    </w:tblBorders>
</w:tblPr>
```

### Table Cell Margins

```xml
<w:tblCellMar>
    <w:top w:w="72" w:type="dxa"/>
    <w:left w:w="115" w:type="dxa"/>
    <w:bottom w:w="72" w:type="dxa"/>
    <w:right w:w="115" w:type="dxa"/>
</w:tblCellMar>
```

### Row Properties (w:trPr)

```xml
<w:tr>
    <w:trPr>
        <w:trHeight w:val="400" w:hRule="atLeast"/>  <!-- Row height -->
        <w:tblHeader/>                                 <!-- Repeat as header -->
        <w:cantSplit/>                                 <!-- Don't split across pages -->
    </w:trPr>
    <!-- cells -->
</w:tr>
```

### Cell Properties (w:tcPr)

```xml
<w:tc>
    <w:tcPr>
        <w:tcW w:w="2880" w:type="dxa"/>           <!-- Cell width -->
        <w:gridSpan w:val="2"/>                      <!-- Span 2 columns -->
        <w:vMerge w:val="restart"/>                  <!-- Start vertical merge -->
        <w:vMerge/>                                   <!-- Continue vertical merge -->
        <w:shd w:val="clear" w:color="auto" w:fill="E0E0E0"/>  <!-- Background -->
        <w:vAlign w:val="center"/>                   <!-- Vertical align: top|center|bottom -->
        <w:tcBorders>
            <w:bottom w:val="single" w:sz="4" w:color="2E74B5"/>
        </w:tcBorders>
    </w:tcPr>
    <w:p><w:r><w:t>Content</w:t></w:r></w:p>
</w:tc>
```

### Table Width Types

| Type | Meaning |
|------|---------|
| `pct` | Percentage (5000 = 100%) |
| `dxa` | Twips |
| `auto` | Auto-fit |
| `nil` | No width |

---

## Lists and Numbering

### Numbering Definition (word/numbering.xml)

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<w:numbering xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">
    <!-- Bullet list abstract definition -->
    <w:abstractNum w:abstractNumId="0">
        <w:nsid w:val="00000001"/>
        <w:multiLevelType w:val="hybridMultilevel"/>
        <w:lvl w:ilvl="0">
            <w:start w:val="1"/>
            <w:numFmt w:val="bullet"/>
            <w:lvlText w:val="&#x2022;"/>
            <w:lvlJc w:val="left"/>
            <w:pPr>
                <w:ind w:left="720" w:hanging="360"/>
            </w:pPr>
            <w:rPr>
                <w:rFonts w:ascii="Symbol" w:hAnsi="Symbol" w:hint="default"/>
            </w:rPr>
        </w:lvl>
        <w:lvl w:ilvl="1">
            <w:start w:val="1"/>
            <w:numFmt w:val="bullet"/>
            <w:lvlText w:val="o"/>
            <w:lvlJc w:val="left"/>
            <w:pPr>
                <w:ind w:left="1440" w:hanging="360"/>
            </w:pPr>
            <w:rPr>
                <w:rFonts w:ascii="Courier New" w:hAnsi="Courier New" w:hint="default"/>
            </w:rPr>
        </w:lvl>
    </w:abstractNum>

    <!-- Numbered list abstract definition -->
    <w:abstractNum w:abstractNumId="1">
        <w:nsid w:val="00000002"/>
        <w:multiLevelType w:val="hybridMultilevel"/>
        <w:lvl w:ilvl="0">
            <w:start w:val="1"/>
            <w:numFmt w:val="decimal"/>
            <w:lvlText w:val="%1."/>
            <w:lvlJc w:val="left"/>
            <w:pPr>
                <w:ind w:left="720" w:hanging="360"/>
            </w:pPr>
        </w:lvl>
    </w:abstractNum>

    <!-- Concrete instances -->
    <w:num w:numId="1">
        <w:abstractNumId w:val="0"/>
    </w:num>
    <w:num w:numId="2">
        <w:abstractNumId w:val="1"/>
    </w:num>
</w:numbering>
```

### Bullet List Item in Document

```xml
<w:p>
    <w:pPr>
        <w:numPr>
            <w:ilvl w:val="0"/>
            <w:numId w:val="1"/>
        </w:numPr>
    </w:pPr>
    <w:r><w:t>Bullet item</w:t></w:r>
</w:p>
```

### Numbered List Item

```xml
<w:p>
    <w:pPr>
        <w:numPr>
            <w:ilvl w:val="0"/>
            <w:numId w:val="2"/>
        </w:numPr>
    </w:pPr>
    <w:r><w:t>Numbered item</w:t></w:r>
</w:p>
```

### Number Formats (w:numFmt)

| Value | Result |
|-------|--------|
| `bullet` | Bullet character |
| `decimal` | 1, 2, 3 |
| `upperLetter` | A, B, C |
| `lowerLetter` | a, b, c |
| `upperRoman` | I, II, III |
| `lowerRoman` | i, ii, iii |

### Content Types Entry for Numbering

Add to `[Content_Types].xml`:
```xml
<Override PartName="/word/numbering.xml" ContentType="application/vnd.openxmlformats-officedocument.wordprocessingml.numbering+xml"/>
```

Add to `word/_rels/document.xml.rels`:
```xml
<Relationship Id="rId4" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/numbering" Target="numbering.xml"/>
```

---

## Styles

### Style Definition (word/styles.xml)

```xml
<w:style w:type="paragraph" w:styleId="CustomHeading">
    <w:name w:val="Custom Heading"/>
    <w:basedOn w:val="Normal"/>
    <w:next w:val="Normal"/>
    <w:qFormat/>
    <w:pPr>
        <w:keepNext/>
        <w:keepLines/>
        <w:spacing w:before="240" w:after="120"/>
        <w:pBdr>
            <w:bottom w:val="single" w:sz="4" w:space="1" w:color="2E74B5"/>
        </w:pBdr>
    </w:pPr>
    <w:rPr>
        <w:rFonts w:ascii="Calibri Light" w:hAnsi="Calibri Light"/>
        <w:b/>
        <w:color w:val="2E74B5"/>
        <w:sz w:val="28"/>
    </w:rPr>
</w:style>
```

### Character Style

```xml
<w:style w:type="character" w:styleId="BoldBlue">
    <w:name w:val="Bold Blue"/>
    <w:rPr>
        <w:b/>
        <w:color w:val="2E74B5"/>
    </w:rPr>
</w:style>
```

### Table Style

```xml
<w:style w:type="table" w:styleId="CustomTable">
    <w:name w:val="Custom Table"/>
    <w:basedOn w:val="TableNormal"/>
    <w:tblPr>
        <w:tblBorders>
            <w:top w:val="single" w:sz="4" w:color="2E74B5"/>
            <w:bottom w:val="single" w:sz="4" w:color="2E74B5"/>
        </w:tblBorders>
    </w:tblPr>
    <w:tblStylePr w:type="firstRow">
        <w:rPr><w:b/></w:rPr>
        <w:tcPr>
            <w:shd w:val="clear" w:color="auto" w:fill="2E74B5"/>
        </w:tcPr>
    </w:tblStylePr>
</w:style>
```

### Style Types

| Type | Purpose |
|------|---------|
| `paragraph` | Applied to paragraphs (via w:pStyle) |
| `character` | Applied to runs (via w:rStyle) |
| `table` | Applied to tables (via w:tblStyle) |
| `numbering` | List formatting |

---

## Headers and Footers

### Add to [Content_Types].xml

```xml
<Override PartName="/word/header1.xml" ContentType="application/vnd.openxmlformats-officedocument.wordprocessingml.header+xml"/>
<Override PartName="/word/footer1.xml" ContentType="application/vnd.openxmlformats-officedocument.wordprocessingml.footer+xml"/>
```

### Add to word/_rels/document.xml.rels

```xml
<Relationship Id="rId10" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/header" Target="header1.xml"/>
<Relationship Id="rId11" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/footer" Target="footer1.xml"/>
```

### Header File (word/header1.xml)

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<w:hdr xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">
    <w:p>
        <w:pPr>
            <w:jc w:val="center"/>
        </w:pPr>
        <w:r>
            <w:t>Document Header</w:t>
        </w:r>
    </w:p>
</w:hdr>
```

### Footer with Page Number (word/footer1.xml)

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<w:ftr xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">
    <w:p>
        <w:pPr>
            <w:jc w:val="center"/>
        </w:pPr>
        <w:r>
            <w:t xml:space="preserve">Page </w:t>
        </w:r>
        <w:r>
            <w:fldChar w:fldCharType="begin"/>
        </w:r>
        <w:r>
            <w:instrText xml:space="preserve"> PAGE </w:instrText>
        </w:r>
        <w:r>
            <w:fldChar w:fldCharType="separate"/>
        </w:r>
        <w:r>
            <w:t>1</w:t>
        </w:r>
        <w:r>
            <w:fldChar w:fldCharType="end"/>
        </w:r>
        <w:r>
            <w:t xml:space="preserve"> of </w:t>
        </w:r>
        <w:r>
            <w:fldChar w:fldCharType="begin"/>
        </w:r>
        <w:r>
            <w:instrText xml:space="preserve"> NUMPAGES </w:instrText>
        </w:r>
        <w:r>
            <w:fldChar w:fldCharType="separate"/>
        </w:r>
        <w:r>
            <w:t>1</w:t>
        </w:r>
        <w:r>
            <w:fldChar w:fldCharType="end"/>
        </w:r>
    </w:p>
</w:ftr>
```

### Reference in Section Properties

```xml
<w:sectPr>
    <w:headerReference w:type="default" r:id="rId10"/>
    <w:footerReference w:type="default" r:id="rId11"/>
    <w:pgSz w:w="12240" w:h="15840"/>
    <w:pgMar w:top="1440" w:right="1440" w:bottom="1440" w:left="1440" w:header="720" w:footer="720"/>
</w:sectPr>
```

### Header/Footer Types

| Type | Purpose |
|------|---------|
| `default` | Used for all pages (unless others specified) |
| `first` | First page only |
| `even` | Even pages only |

---

## Hyperlinks

### Add to word/_rels/document.xml.rels

```xml
<Relationship Id="rId20" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/hyperlink" Target="https://example.com" TargetMode="External"/>
```

### Hyperlink in Document

```xml
<w:hyperlink r:id="rId20" w:history="1">
    <w:r>
        <w:rPr>
            <w:rStyle w:val="Hyperlink"/>
            <w:color w:val="0563C1"/>
            <w:u w:val="single"/>
        </w:rPr>
        <w:t>Click here</w:t>
    </w:r>
</w:hyperlink>
```

### Internal Bookmark Link

```xml
<!-- Define bookmark -->
<w:bookmarkStart w:id="0" w:name="section1"/>
<w:r><w:t>Section 1 Content</w:t></w:r>
<w:bookmarkEnd w:id="0"/>

<!-- Link to bookmark -->
<w:hyperlink w:anchor="section1">
    <w:r>
        <w:rPr>
            <w:color w:val="0563C1"/>
            <w:u w:val="single"/>
        </w:rPr>
        <w:t>Go to Section 1</w:t>
    </w:r>
</w:hyperlink>
```

---

## Images

### Add to [Content_Types].xml

```xml
<Default Extension="png" ContentType="image/png"/>
<Default Extension="jpeg" ContentType="image/jpeg"/>
<Default Extension="jpg" ContentType="image/jpeg"/>
```

### Add to word/_rels/document.xml.rels

```xml
<Relationship Id="rId30" Type="http://schemas.openxmlformats.org/officeDocument/2006/relationships/image" Target="media/image1.png"/>
```

### Inline Image in Document

```xml
<w:r>
    <w:drawing>
        <wp:inline distT="0" distB="0" distL="0" distR="0"
            xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing">
            <wp:extent cx="914400" cy="914400"/>  <!-- Size in EMUs (1 inch) -->
            <wp:docPr id="1" name="Picture 1"/>
            <a:graphic xmlns:a="http://schemas.openxmlformats.org/drawingml/2006/main">
                <a:graphicData uri="http://schemas.openxmlformats.org/drawingml/2006/picture">
                    <pic:pic xmlns:pic="http://schemas.openxmlformats.org/drawingml/2006/picture">
                        <pic:nvPicPr>
                            <pic:cNvPr id="0" name="image1.png"/>
                            <pic:cNvPicPr/>
                        </pic:nvPicPr>
                        <pic:blipFill>
                            <a:blip r:embed="rId30"
                                xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"/>
                            <a:stretch>
                                <a:fillRect/>
                            </a:stretch>
                        </pic:blipFill>
                        <pic:spPr>
                            <a:xfrm>
                                <a:off x="0" y="0"/>
                                <a:ext cx="914400" cy="914400"/>
                            </a:xfrm>
                            <a:prstGeom prst="rect">
                                <a:avLst/>
                            </a:prstGeom>
                        </pic:spPr>
                    </pic:pic>
                </a:graphicData>
            </a:graphic>
        </wp:inline>
    </w:drawing>
</w:r>
```

### Image Size Calculations

- 1 inch = 914400 EMUs
- Width/height in EMUs = pixels * 914400 / 96 (assuming 96 DPI)

---

## Fields

### Page Number Field

```xml
<w:r>
    <w:fldChar w:fldCharType="begin"/>
</w:r>
<w:r>
    <w:instrText xml:space="preserve"> PAGE </w:instrText>
</w:r>
<w:r>
    <w:fldChar w:fldCharType="separate"/>
</w:r>
<w:r>
    <w:t>1</w:t>  <!-- Cached display value -->
</w:r>
<w:r>
    <w:fldChar w:fldCharType="end"/>
</w:r>
```

### Total Pages Field

```xml
<w:r><w:fldChar w:fldCharType="begin"/></w:r>
<w:r><w:instrText xml:space="preserve"> NUMPAGES </w:instrText></w:r>
<w:r><w:fldChar w:fldCharType="separate"/></w:r>
<w:r><w:t>1</w:t></w:r>
<w:r><w:fldChar w:fldCharType="end"/></w:r>
```

### Date Field

```xml
<w:r><w:fldChar w:fldCharType="begin"/></w:r>
<w:r><w:instrText xml:space="preserve"> DATE \@ "MMMM d, yyyy" </w:instrText></w:r>
<w:r><w:fldChar w:fldCharType="separate"/></w:r>
<w:r><w:t>January 1, 2025</w:t></w:r>
<w:r><w:fldChar w:fldCharType="end"/></w:r>
```

### Table of Contents Field

```xml
<w:p>
    <w:r><w:fldChar w:fldCharType="begin"/></w:r>
    <w:r><w:instrText xml:space="preserve"> TOC \o "1-3" \h \z \u </w:instrText></w:r>
    <w:r><w:fldChar w:fldCharType="separate"/></w:r>
    <!-- TOC entries appear here when updated -->
    <w:r><w:fldChar w:fldCharType="end"/></w:r>
</w:p>
```

### Common Field Codes

| Code | Purpose |
|------|---------|
| `PAGE` | Current page number |
| `NUMPAGES` | Total pages |
| `DATE` | Current date |
| `TIME` | Current time |
| `AUTHOR` | Document author |
| `TITLE` | Document title |
| `TOC` | Table of contents |
| `REF` | Cross-reference |

---

## Section Properties

### Full Section Properties

```xml
<w:sectPr>
    <w:headerReference w:type="default" r:id="rId10"/>
    <w:footerReference w:type="default" r:id="rId11"/>
    <w:pgSz w:w="12240" w:h="15840" w:orient="portrait"/>
    <w:pgMar w:top="1440" w:right="1440" w:bottom="1440" w:left="1440"
             w:header="720" w:footer="720" w:gutter="0"/>
    <w:cols w:space="720"/>  <!-- Column spacing -->
    <w:docGrid w:linePitch="360"/>
    <w:titlePg/>  <!-- Different first page -->
</w:sectPr>
```

### Landscape Orientation

```xml
<w:pgSz w:w="15840" w:h="12240" w:orient="landscape"/>
```

### Two-Column Layout

```xml
<w:cols w:num="2" w:space="720"/>
```

### Section Break (mid-document)

```xml
<w:p>
    <w:pPr>
        <w:sectPr>
            <w:type w:val="nextPage"/>  <!-- nextPage | continuous | evenPage | oddPage -->
            <w:pgSz w:w="12240" w:h="15840"/>
            <w:pgMar w:top="1440" w:right="1440" w:bottom="1440" w:left="1440"/>
        </w:sectPr>
    </w:pPr>
</w:p>
```

---

## Element Reference Tables

### All Run Properties (w:rPr)

| Element | Purpose | Example |
|---------|---------|---------|
| `w:b` | Bold | `<w:b/>` |
| `w:bCs` | Bold (complex script) | `<w:bCs/>` |
| `w:i` | Italic | `<w:i/>` |
| `w:iCs` | Italic (complex script) | `<w:iCs/>` |
| `w:caps` | All caps | `<w:caps/>` |
| `w:smallCaps` | Small caps | `<w:smallCaps/>` |
| `w:strike` | Strikethrough | `<w:strike/>` |
| `w:dstrike` | Double strikethrough | `<w:dstrike/>` |
| `w:outline` | Outline text | `<w:outline/>` |
| `w:shadow` | Shadow | `<w:shadow/>` |
| `w:emboss` | Emboss | `<w:emboss/>` |
| `w:imprint` | Imprint/engrave | `<w:imprint/>` |
| `w:vanish` | Hidden text | `<w:vanish/>` |
| `w:color` | Text color | `<w:color w:val="FF0000"/>` |
| `w:sz` | Font size (half-points) | `<w:sz w:val="24"/>` (12pt) |
| `w:szCs` | Complex script font size | `<w:szCs w:val="24"/>` |
| `w:rFonts` | Font family | `<w:rFonts w:ascii="Arial" w:hAnsi="Arial"/>` |
| `w:u` | Underline | `<w:u w:val="single"/>` |
| `w:highlight` | Highlight color | `<w:highlight w:val="yellow"/>` |
| `w:vertAlign` | Super/subscript | `<w:vertAlign w:val="superscript"/>` |
| `w:spacing` | Character spacing | `<w:spacing w:val="20"/>` (twips) |
| `w:w` | Character width | `<w:w w:val="150"/>` (%) |
| `w:position` | Vertical position | `<w:position w:val="6"/>` |
| `w:lang` | Language | `<w:lang w:val="en-US"/>` |

### All Paragraph Properties (w:pPr)

| Element | Purpose | Example |
|---------|---------|---------|
| `w:pStyle` | Paragraph style | `<w:pStyle w:val="Heading1"/>` |
| `w:jc` | Alignment | `<w:jc w:val="center"/>` |
| `w:ind` | Indentation | `<w:ind w:left="720" w:firstLine="360"/>` |
| `w:spacing` | Spacing | `<w:spacing w:before="240" w:after="120"/>` |
| `w:keepNext` | Keep with next | `<w:keepNext/>` |
| `w:keepLines` | Keep lines together | `<w:keepLines/>` |
| `w:pageBreakBefore` | Page break before | `<w:pageBreakBefore/>` |
| `w:widowControl` | Widow/orphan control | `<w:widowControl w:val="0"/>` |
| `w:numPr` | Numbering | `<w:numPr><w:numId w:val="1"/></w:numPr>` |
| `w:pBdr` | Borders | `<w:pBdr><w:bottom.../></w:pBdr>` |
| `w:shd` | Shading | `<w:shd w:fill="FFFF00"/>` |
| `w:tabs` | Tab stops | `<w:tabs><w:tab w:val="left" w:pos="720"/></w:tabs>` |
| `w:outlineLvl` | Outline level | `<w:outlineLvl w:val="0"/>` |
| `w:contextualSpacing` | Contextual spacing | `<w:contextualSpacing/>` |
| `w:bidi` | Bidirectional | `<w:bidi/>` |

### Underline Values (w:u w:val)

| Value | Description |
|-------|-------------|
| `single` | Single underline |
| `double` | Double underline |
| `thick` | Thick underline |
| `dotted` | Dotted underline |
| `dash` | Dashed underline |
| `dotDash` | Dot-dash underline |
| `wave` | Wavy underline |
| `words` | Words only |
| `none` | No underline |

### Highlight Colors (w:highlight w:val)

| Value | Color |
|-------|-------|
| `yellow` | Yellow |
| `green` | Green |
| `cyan` | Cyan |
| `magenta` | Magenta |
| `blue` | Blue |
| `red` | Red |
| `darkBlue` | Dark blue |
| `darkCyan` | Dark cyan |
| `darkGreen` | Dark green |
| `darkMagenta` | Dark magenta |
| `darkRed` | Dark red |
| `darkYellow` | Dark yellow |
| `darkGray` | Dark gray |
| `lightGray` | Light gray |
| `black` | Black |

### Border Values (w:val)

| Value | Description |
|-------|-------------|
| `single` | Single line |
| `double` | Double line |
| `thick` | Thick line |
| `dotted` | Dotted line |
| `dashed` | Dashed line |
| `nil` | No border |
| `threeDEmboss` | 3D emboss |
| `threeDEngrave` | 3D engrave |
| `wave` | Wave |

### XML Escaping

Always escape these characters in text content:
| Character | Escape |
|-----------|--------|
| `&` | `&amp;` |
| `<` | `&lt;` |
| `>` | `&gt;` |
| `"` | `&quot;` |
| `'` | `&apos;` |
