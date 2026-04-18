---
name: standardize-chinese-document-punctuation
description: Standardize punctuation, spacing, and clear superscript/subscript notation in Chinese formal documents, plans, proposals, reports, academic papers, official/business writing, and mixed Chinese-English text while preserving bibliography/reference sections and citation markers. Use when the user asks to normalize Chinese punctuation, remove unwanted spaces between Chinese and English or numbers, clean plan-book or paper body text, polish document formatting conventions, format chemical formulas, ion charges, powers/exponents, squared/cubed units, or apply a consistent Chinese writing standard across .docx, .pdf, .md, .txt, spreadsheet text, or pasted content. When ambiguous superscript/subscript decisions involve chemical formulas, units, or standard notation and web access is allowed, use conditional authoritative web lookup instead of guessing.
---

# Standardize Chinese Document Punctuation

## Purpose

Apply a formal Chinese document style to正文 text: Chinese context uses full-width Chinese punctuation, Chinese-English and Chinese-number boundaries normally have no spaces, clear chemical/math/unit notation uses appropriate superscript or subscript, and English phrases keep their internal spelling and spacing.

Use this skill together with the relevant file-format skill when editing files, such as the DOCX, PDF, or spreadsheet skill. Preserve layout, styles, tables, fields, formula objects, URLs, code, paths, identifiers, reference sections, and citation markers unless the user explicitly asks to edit them.

## Workflow

1. Identify the editing scope. Default to正文 text only for plans, proposals, reports, and academic papers; avoid changing cover pages, signatures, legal names, tables of contents, references, formulas, code blocks, URLs, file paths, and raw data fields unless requested.
2. Freeze protected spans before editing: bibliography/reference sections, citation markers, footnotes, endnotes, URLs, code, file paths, formula objects, table keys, and raw data fields.
3. Normalize clear superscript/subscript notation in the remaining正文 only.
4. For ambiguous but high-value superscript/subscript decisions, perform conditional authoritative web lookup when web access is allowed and the user has not forbidden browsing.
5. Normalize spacing, then punctuation, then do a final consistency pass.
6. Preserve meaning. Do not rewrite sentences, translate terms, expand acronyms, or change numbers while applying punctuation, spacing, and superscript/subscript rules.
7. If a file format has visible layout, render or inspect the result when possible to ensure no text overflow or broken formatting was introduced.

## Academic Papers

For academic papers, theses, journal manuscripts, and research reports, apply this skill to main正文 only.

Do not edit bibliography or reference-list sections headed by labels such as:

- `参考文献`
- `References`
- `Bibliography`
- `Works Cited`
- `参考资料`

Do not alter citation markers in正文, footnotes, endnotes, captions, tables, or figure notes. Preserve their original punctuation, spacing, brackets, superscript formatting, and numbering. Examples include:

- Numeric citations: `[1]`, `[1-3]`, `[1, 3, 5]`, `［1］`
- Superscript citation numbers or footnote markers.
- Author-year citations: `(Smith, 2020)`, `（Smith, 2020）`, `（张三，2020）`

If citation punctuation conflicts with this skill's Chinese punctuation rules, preserve the citation as-is.

For `.docx` academic documents that use Word cross-references or fields for numeric citation markers, preserve the whole citation marker as a citation unit. If a citation marker is superscripted, every visible and field-related run in the marker must remain superscripted, including brackets, commas, hyphens, field begin/separate/end runs, field instruction runs, and the displayed field-result number runs between `w:fldCharType="separate"` and `w:fldCharType="end"`. Do not rely on the field-code run's superscript formatting alone, because Word field updates can regenerate the displayed result run as baseline text.

When creating or repairing Word REF citation fields, prefer adding a formatting-preservation switch such as `\* MERGEFORMAT` or `\* CHARFORMAT`, then update fields, then perform a final pass that confirms all displayed REF field-result number runs inside citation markers still have `w:vertAlign w:val="superscript"` when the surrounding citation marker is superscripted. Preserve the REF field and bibliography bookmark structure; do not replace cross-references with static text unless the user explicitly asks.

## Superscript and Subscript Rules

Apply these rules conservatively. Do not let superscript/subscript normalization override reference, citation, footnote, endnote, URL, code, path, version, model-number, product-name, gene/protein-name, or document-ID protection.

Choose output by file type:

- `.docx`, `.pptx`, `.xlsx`: use true superscript/subscript formatting while preserving surrounding font, size, color, paragraph style, and table layout.
- `.html`: use `<sup>` and `<sub>`.
- `.md`, `.txt`, pasted text, and other plain text: use Unicode superscript/subscript characters for safe numeric and sign notation; if Unicode cannot represent the expression reliably, preserve the original notation and mention it.
- Existing Word equation objects, MathType objects, LaTeX math blocks, and other formula objects: do not rewrite or flatten them unless the user explicitly asks.

Chemical formulas:

- Treat numeric counts after element symbols or closing parentheses as subscripts in clear chemical formulas: `H2O` -> `H₂O`, `CO2` -> `CO₂`, `Na2SO4` -> `Na₂SO₄`, `Ca(OH)2` -> `Ca(OH)₂`.
- Preserve leading stoichiometric coefficients as normal baseline numbers: `2H2O` -> `2H₂O`.
- For hydrates, keep the hydrate coefficient baseline and subscript the molecule counts: `CuSO4·5H2O` -> `CuSO₄·5H₂O`.

Ion charges and oxidation states:

- Use subscripts for chemical counts and superscripts for charges: `NH4+` -> `NH₄⁺`, `Fe3+` -> `Fe³⁺`, `SO4^2-` -> `SO₄²⁻`.
- Do not convert a trailing `+` or `-` to charge notation unless the expression is clearly an ion or chemical species.

Powers, exponents, and units:

- Treat explicit exponent notation as superscript in math/unit context: `x^2`, `10^6`, `(a+b)^2`, `m^2/s^2`.
- In plain text, convert only safe numeric/sign exponents to Unicode, such as `10^6` -> `10⁶` and `m^2/s^2` -> `m²/s²`. Preserve alphabetic or complex exponents that Unicode cannot represent cleanly.
- Treat clear squared/cubed units as superscript: `20 m2` -> `20 m²`, `3 cm3` -> `3 cm³`.
- Do not infer exponents from product names, versions, model numbers, labels, or identifiers.

Default exclusions:

- Preserve likely gene/protein/cell-line and biomedical identifiers such as `H2AX`, `p53`, `C2C12`, and `IL-6`.
- Preserve versions and model/product names such as `v2.0`, `Model 3`, `ISO 9001`, and `Windows 11`.
- Preserve author-defined variables when context does not make the superscript/subscript role clear.

## Conditional Web Lookup

Use web lookup only when it can materially improve a high-ambiguity superscript/subscript decision and web access is allowed. Prefer preserving the original text over guessing.

Browse for authoritative confirmation only in these cases:

- An expression may be a chemical formula, gene/protein name, material model, or product identifier, such as `H2AX`, `C2C12`, or `P2O5`.
- Ion charge, oxidation state, hydrate notation, or compound notation is unclear, such as `Fe2+` or `CuSO4·5H2O`.
- A complex unit expression may require standard SI or discipline-specific exponent formatting.
- The user explicitly asks to check the standard notation, verify the formula, or judge automatically.

Do not browse for:

- Obvious citation markers, footnotes, endnotes, and bibliography/reference sections.
- Obvious URLs, code, paths, versions, model numbers, serial numbers, or document IDs.
- Author-defined variables whose intended notation cannot be confirmed by public authoritative sources.

Source priority:

- Chemical formulas and compounds: PubChem, NIST Chemistry WebBook, IUPAC, or authoritative journal/textbook sources.
- Units and SI notation: BIPM/SI, NIST, ISO, or relevant national standards.
- Paper formatting: the target journal, conference, publisher, or school thesis-format guide.

Use lookup results only to decide whether superscript/subscript formatting is appropriate. Do not rewrite bibliography entries, citation formats, or author-defined notation based solely on external search results. If authoritative sources do not resolve the ambiguity, keep the original text and report the uncertain item.

## Spacing Rules

Remove spaces at Chinese-Latin and Chinese-number boundaries in Chinese正文:

- `本项目采用 AI 技术。` -> `本项目采用AI技术。`
- `周期为 3 个月。` -> `周期为3个月。`
- `预算为 100 万元。` -> `预算为100万元。`
- `覆盖率达到 95 %。` -> `覆盖率达到95%。`

Keep spaces that belong inside English text or names:

- Keep: `Project Management Office`
- Keep: `Microsoft Office`
- Keep: `OpenAI API`
- Keep: `CPU 3.2 GHz`
- Keep: `5 MB/s`

Clean accidental whitespace:

- Collapse repeated spaces inside Chinese paragraphs unless the spaces are part of English text, code, alignment, tables, or fixed-width formatting.
- Remove leading and trailing spaces around paragraphs and cells.
- Do not remove line breaks that separate paragraphs, list items, table rows, or headings.

## Punctuation Rules

Use Chinese full-width punctuation in Chinese context:

- `，` for comma, `。` for period, `；` for semicolon, `：` for colon, `？` for question mark, `！` for exclamation mark.
- `（ ）` for parentheses in Chinese text: `项目管理办公室（PMO）负责统筹。`
- `“ ”` for Chinese quotation marks.
- `《 》` for book, policy, plan, report, and document titles.
- `、` for Chinese-style short parallel items.
- `……` for ellipsis in Chinese text.

Use half-width punctuation only where it is part of an English, technical, or machine-readable expression:

- English sentences: `The system is ready for deployment.`
- Versions and decimals: `Version 2.0`, `3.14`
- API routes, URLs, emails, file paths, commands, code, identifiers: `/v1/tasks`, `name@example.com`, `C:\data\plan.docx`
- Technical values: `CPU 3.2 GHz`, `5 MB/s`

In Chinese sentences containing English words, use Chinese punctuation around the sentence:

- `本项目采用AI、大数据和云计算技术。`
- `项目管理办公室（PMO）负责统筹实施。`
- `系统支持Windows、macOS、Linux。`

Prefer a Chinese colon for labels in Chinese text:

- `项目目标：提升流程效率。`
- `实施周期：3个月。`

## Guardrails

Do not alter:

- Brand names, legal names, product names, acronyms, and official titles.
- Bibliography/reference sections and citation markers, including numeric citations, author-year citations, superscripts, footnotes, and endnotes.
- Numeric values, units, dates, monetary amounts, percentages, and ranges.
- Hyperlinks, citations, footnote markers, field codes, formula objects, source code, JSON, command lines, table keys, and filenames.
- Versions, model numbers, product identifiers, gene/protein names, biomedical identifiers, and document IDs unless the user explicitly asks and the notation is confirmed.
- English-only paragraphs, except to fix obvious accidental Chinese punctuation only when requested.

When uncertain whether a half-width mark or baseline number is technical syntax, citation notation, identifier text, or ordinary punctuation/notation, preserve it and mention the ambiguity instead of risking data corruption.

## Final Check

Before finishing, scan for these common issues:

- Chinese character followed by a space then Latin letters or digits.
- Latin letters or digits followed by a space then Chinese character.
- Half-width punctuation adjacent to Chinese正文 where full-width punctuation should be used.
- Full-width punctuation inside URLs, code, paths, emails, decimals, or version numbers.
- Repeated spaces, leading spaces, and trailing spaces in edited正文.
- Chemical counts that should clearly be subscripts, such as `H2O`, `CO2`, `Na2SO4`, and `Ca(OH)2`.
- Clear charge/exponent/unit notation that should be superscript, such as `NH4+`, `SO4^2-`, `x^2`, `10^6`, `m2`, and `cm3`.
- Accidental edits to references, citations, footnotes, endnotes, gene/protein names, versions, models, URLs, code, and document IDs.
- For `.docx` files with Word REF cross-reference citation fields, no citation field result number between `w:fldCharType="separate"` and `w:fldCharType="end"` should lose superscript formatting when the citation marker is superscripted; verify this after any Word `Fields.Update()` or PDF export.
