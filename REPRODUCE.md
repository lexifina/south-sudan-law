# How this repository was made (South Sudan)

This file is written by the build on 2026-10-30, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| Ministry of Justice and Constitutional Affairs (MoJCA): Laws of the Republic of South Sudan, read through Internet Archive captures | <https://mojca.gov.ss/laws-of-the-republic-of-south-sudan/> | 2026-10-28 | © Copyright. Ministry of Justice and Constitutional Affairs (MoJCA). 2023. All Rights Reserved. |
| WIPO Lex (World Intellectual Property Organization), South Sudan records SS013, SS018, SS019 | <https://www.wipo.int/wipolex/en/legislation/details/21916> | 2026-10-28 | WIPO Lex terms of use; only the records' dates and notes are used, not WIPO's texts |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | The Transitional Constitution of the Republic of South Sudan, 2011 | 1 | 2011-07-09 to 2011-07-09 |
| `penal-code` | The Penal Code Act, 2008 (Act 9 of 2008) | 1 | 2008-08-22 to 2008-08-22 |
| `criminal-procedure` | The Code of Criminal Procedure Act, 2008 (Act 5 of 2008) | 1 | 2008-03-20 to 2008-03-20 |

The build made 3 commits:

| Commits | Kind |
| ---: | --- |
| 3 | first version of an act |
| 0 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-30.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 3 laws in the record.
- 6 tags.

## Dates

Each commit is dated at noon (Africa/Juba) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: No general rule is applied. Each act here states its own commencement: the Penal Code Act 2008 (s. 1) and the Code of Criminal Procedure Act 2008 (s. 1) come into force on the date of the President's signature, given in the gazette's margin note; the Transitional Constitution 2011 (Art. 198) comes into force on July 9, 2011. https://mojca.gov.ss/laws-of-the-republic-of-south-sudan/

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `ae686143ab019e40c29982c554fc9feed4fecc73b254d5ca8081e60bf11464d3` (817212 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3e59cb6f05eccb94a9ec14431a7f6781221e83ef`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

Not yet run for this build.

No second build of this corpus has been compared yet.

## Decisions made by hand

- Constitution text: the ministry's 'LAWS OF SOUTH SUDAN' print (uploads/2023/03, 203 articles, PDF made 12 July 2011). The ministry's second copy under the same title (uploads/2023/04, 201 articles) is a Word file made on 24 April 2011 by sudantribune.com, before the Assembly approved the text on 7 July 2011; WIPO Lex SS013 is the same file. It was not used. The 203-article print agrees with the constituteproject.org text (WIPO Lex SS019) on its article numbering and Art. 100, which was read only to reconcile, never copied.
- In force 9 July 2011 (Art. 198: 'shall come into force on July 9, 2011'); WIPO Lex SS013 records approval on 7 July 2011 and assent on 9 July 2011. The print's assent formula has its date left blank ('this ---- day of the month of ---- in the year 2011') and is kept as printed, as the unit 'assent'.
- Units are articles (art-NNN) with the article title as the heading, the preamble with its enacting formula, Schedules (A) to (E) and the assent. Part and chapter headings and the arrangement of articles are left out.
- Only the 2011 text is built. The Transitional Constitution of the Republic of South Sudan, 2011 (Amendment) Act, 2013 (assented 26 February 2013, commenced 1 March 2013, per WIPO Lex SS018) is published only as a scan with no text layer, and is left out (no OCR). The Labour Act 2017 cites the Constitution as '(Amended 2015)', so a 2015 amendment exists too; no official text of it was found. Later amendments are not on the ministry's list either.
- So this act stops at its text as signed and is not published to main: today's text of the Constitution is not available from an official source with a text layer.
- Source: the certificate check was not bypassed.
- Phase 1 acts: the Transitional Constitution 2011, the Penal Code Act 2008 and the Code of Criminal Procedure Act 2008. The two codes were chosen because their gazette print (Acts Supplement No. 1 to the Southern Sudan Gazette No. 1 Vol. I, 10 February 2009) has a text layer and dates each act by a 'Signed on' margin note. The Labour Act 2017 was not built: its print ('Juba, 24th October 2017') does not say the President signed it that day, and it comes into force on signature.
- Penal Code Act 2008: in force 22 August 2008, the day the President signed it (s. 1: 'shall come into force on the date of its signature by the President'; margin note 'Signed on 22nd August, 2008'). Published 10 February 2009.
- Code of Criminal Procedure Act 2008: in force 20 March 2008 (s. 1: 'shall come into force as from the date of its signature by the President'; margin note 'Signed on 20th March, 2008'). Published 10 February 2009.
- Each code is one version: the act as enacted. The ministry's list (latest capture 27 July 2026) offers no amending act and no consolidated text for either code, so the enacted text is the latest official expression available. An amendment that exists but is not on the list is not in this history.
- Units are sections (sec-NNN) headed '# Section N — Title'. Chapter headings, the arrangement of sections, running heads, page numbers and the 'Signed on' margin notes are left out of the text; the enacting formula is the unit 'preamble'.
- Paragraphs are rebuilt from the PDF line layout: a line holding only a marker ('(1)', '(a)') is joined to the text after it, and lines are joined across line and page breaks until a paragraph ends in . ; : or a dash. A hyphen at a line end is kept and the next word joined to it, since the print does not distinguish hyphenated words from broken ones.
- Quotes are normalised to straight quotes; NBSP and runs of spaces become one space. No word of the law was changed.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code with Claude Opus 5.5 (claude-opus-5-5) chose the sources and wrote Lexifina's code. No model read, wrote or changed legal text. Research used 2 web searches; no text was taken from them.
- Claude Sonnet 5.5 (claude-sonnet-5-5) later fixed Lexifina's code (section-heading detection) and ran the build; it read no legal text into the corpus except through Lexifina's code.
